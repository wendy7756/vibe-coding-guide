# IntelliJ IDEA + AI Integration Guide

<div align="center">English | [中文](./intellij-ai-guide.md)</div>

## Overview

IntelliJ IDEA is JetBrains' flagship IDE for Java and JVM-based development. With AI integration, it becomes an incredibly powerful tool for modern Java development, offering intelligent code generation, refactoring suggestions, and automated testing capabilities.

## Installation and Setup

### System Requirements
- IntelliJ IDEA 2023.1 or later
- Java 11 or higher
- Minimum 8GB RAM (16GB recommended)
- Internet connection for AI services

### AI Plugin Installation

#### 1. JetBrains AI Assistant
```bash
# Method 1: Through IDE
Settings → Plugins → Marketplace → Search "AI Assistant" → Install

# Method 2: Manual Installation
Download from JetBrains Plugin Repository
Settings → Plugins → Install from Disk
```

#### 2. GitHub Copilot
```bash
Settings → Plugins → Marketplace → Search "GitHub Copilot" → Install
Restart IDE → Sign in with GitHub account
```

#### 3. Tabnine
```bash
Settings → Plugins → Marketplace → Search "Tabnine" → Install
Configure API key and preferences
```

## Java Development with AI

### 1. Smart Class Generation

#### Service Layer Creation
```java
// AI Prompt: Create a UserService with full CRUD operations
public interface UserService {
    // AI will generate:
    User createUser(CreateUserRequest request);
    User getUserById(Long id);
    User updateUser(Long id, UpdateUserRequest request);
    void deleteUser(Long id);
    Page<User> findUsers(UserSearchCriteria criteria, Pageable pageable);
    boolean existsByEmail(String email);
    List<User> findActiveUsers();
}

// Implementation
@Service
@Transactional
public class UserServiceImpl implements UserService {
    
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    private final UserMapper userMapper;
    
    public UserServiceImpl(UserRepository userRepository, 
                          PasswordEncoder passwordEncoder,
                          UserMapper userMapper) {
        this.userRepository = userRepository;
        this.passwordEncoder = passwordEncoder;
        this.userMapper = userMapper;
    }
    
    @Override
    public User createUser(CreateUserRequest request) {
        if (existsByEmail(request.getEmail())) {
            throw new DuplicateEmailException("Email already exists: " + request.getEmail());
        }
        
        User user = User.builder()
            .email(request.getEmail())
            .username(request.getUsername())
            .password(passwordEncoder.encode(request.getPassword()))
            .firstName(request.getFirstName())
            .lastName(request.getLastName())
            .status(UserStatus.ACTIVE)
            .createdAt(LocalDateTime.now())
            .build();
            
        return userRepository.save(user);
    }
    
    @Override
    @Transactional(readOnly = true)
    public User getUserById(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new UserNotFoundException("User not found: " + id));
    }
    
    // AI generates remaining methods...
}
```

### 2. Spring Framework Integration

#### Controller Generation
```java
// AI Prompt: Create REST controller for user management
@RestController
@RequestMapping("/api/v1/users")
@Validated
@CrossOrigin(origins = {"http://localhost:3000", "https://myapp.com"})
public class UserController {
    
    private final UserService userService;
    
    public UserController(UserService userService) {
        this.userService = userService;
    }
    
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public ResponseEntity<UserResponse> createUser(@Valid @RequestBody CreateUserRequest request) {
        User user = userService.createUser(request);
        UserResponse response = UserResponse.from(user);
        return ResponseEntity.created(URI.create("/api/v1/users/" + user.getId()))
                           .body(response);
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<UserResponse> getUser(@PathVariable @Min(1) Long id) {
        User user = userService.getUserById(id);
        return ResponseEntity.ok(UserResponse.from(user));
    }
    
    @GetMapping
    public ResponseEntity<Page<UserResponse>> getUsers(
            @RequestParam(defaultValue = "0") @Min(0) int page,
            @RequestParam(defaultValue = "20") @Min(1) @Max(100) int size,
            @RequestParam(defaultValue = "id") String sortBy,
            @RequestParam(defaultValue = "ASC") Sort.Direction direction,
            @ModelAttribute UserSearchCriteria criteria) {
        
        Pageable pageable = PageRequest.of(page, size, Sort.by(direction, sortBy));
        Page<User> users = userService.findUsers(criteria, pageable);
        Page<UserResponse> response = users.map(UserResponse::from);
        
        return ResponseEntity.ok(response);
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<UserResponse> updateUser(@PathVariable @Min(1) Long id,
                                                 @Valid @RequestBody UpdateUserRequest request) {
        User user = userService.updateUser(id, request);
        return ResponseEntity.ok(UserResponse.from(user));
    }
    
    @DeleteMapping("/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public ResponseEntity<Void> deleteUser(@PathVariable @Min(1) Long id) {
        userService.deleteUser(id);
        return ResponseEntity.noContent().build();
    }
}
```

### 3. Repository and Entity Generation

#### JPA Entity with AI
```java
// AI Prompt: Create User entity with JPA annotations
@Entity
@Table(name = "users", indexes = {
    @Index(name = "idx_user_email", columnList = "email", unique = true),
    @Index(name = "idx_user_username", columnList = "username"),
    @Index(name = "idx_user_status", columnList = "status"),
    @Index(name = "idx_user_created_at", columnList = "created_at")
})
@EntityListeners(AuditingEntityListener.class)
@Builder
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(name = "email", nullable = false, unique = true, length = 100)
    @Email(message = "Invalid email format")
    private String email;
    
    @Column(name = "username", nullable = false, length = 50)
    @Size(min = 3, max = 50, message = "Username must be between 3 and 50 characters")
    private String username;
    
    @Column(name = "password", nullable = false)
    @JsonIgnore
    private String password;
    
    @Column(name = "first_name", length = 50)
    private String firstName;
    
    @Column(name = "last_name", length = 50)
    private String lastName;
    
    @Enumerated(EnumType.STRING)
    @Column(name = "status", nullable = false)
    private UserStatus status;
    
    @CreatedDate
    @Column(name = "created_at", nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    @Column(name = "updated_at")
    private LocalDateTime updatedAt;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JsonIgnore
    private List<UserRole> roles = new ArrayList<>();
    
    @Version
    private Long version;
    
    // AI generates custom methods
    public boolean isActive() {
        return status == UserStatus.ACTIVE;
    }
    
    public String getFullName() {
        return (firstName != null ? firstName : "") + " " + (lastName != null ? lastName : "");
    }
    
    public void addRole(Role role) {
        UserRole userRole = new UserRole();
        userRole.setUser(this);
        userRole.setRole(role);
        userRole.setAssignedAt(LocalDateTime.now());
        roles.add(userRole);
    }
}

// Repository with AI-generated queries
@Repository
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {
    
    Optional<User> findByEmail(String email);
    
    Optional<User> findByUsername(String username);
    
    boolean existsByEmail(String email);
    
    boolean existsByUsername(String username);
    
    @Query("SELECT u FROM User u WHERE u.status = :status ORDER BY u.createdAt DESC")
    List<User> findByStatus(@Param("status") UserStatus status);
    
    @Query("SELECT u FROM User u WHERE u.status = 'ACTIVE' AND u.createdAt >= :date")
    List<User> findActiveUsersSince(@Param("date") LocalDateTime date);
    
    @Modifying
    @Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
    int updateUserStatus(@Param("id") Long id, @Param("status") UserStatus status);
    
    // AI can generate complex queries
    @Query("""
        SELECT u FROM User u 
        LEFT JOIN FETCH u.roles ur 
        LEFT JOIN FETCH ur.role r 
        WHERE (:email IS NULL OR u.email LIKE %:email%) 
        AND (:status IS NULL OR u.status = :status) 
        AND (:fromDate IS NULL OR u.createdAt >= :fromDate)
        AND (:toDate IS NULL OR u.createdAt <= :toDate)
        """)
    Page<User> findUsersWithCriteria(@Param("email") String email,
                                   @Param("status") UserStatus status,
                                   @Param("fromDate") LocalDateTime fromDate,
                                   @Param("toDate") LocalDateTime toDate,
                                   Pageable pageable);
}
```

### 4. Testing with AI

#### Unit Test Generation
```java
// AI generates comprehensive test suite
@ExtendWith(MockitoExtension.class)
class UserServiceImplTest {
    
    @Mock
    private UserRepository userRepository;
    
    @Mock
    private PasswordEncoder passwordEncoder;
    
    @Mock
    private UserMapper userMapper;
    
    @InjectMocks
    private UserServiceImpl userService;
    
    @Test
    @DisplayName("Should create user successfully when valid request provided")
    void shouldCreateUserSuccessfully() {
        // Given
        CreateUserRequest request = CreateUserRequest.builder()
            .email("test@example.com")
            .username("testuser")
            .password("password123")
            .firstName("John")
            .lastName("Doe")
            .build();
            
        User savedUser = User.builder()
            .id(1L)
            .email(request.getEmail())
            .username(request.getUsername())
            .password("encodedPassword")
            .firstName(request.getFirstName())
            .lastName(request.getLastName())
            .status(UserStatus.ACTIVE)
            .createdAt(LocalDateTime.now())
            .build();
        
        when(userRepository.existsByEmail(request.getEmail())).thenReturn(false);
        when(passwordEncoder.encode(request.getPassword())).thenReturn("encodedPassword");
        when(userRepository.save(any(User.class))).thenReturn(savedUser);
        
        // When
        User result = userService.createUser(request);
        
        // Then
        assertThat(result).isNotNull();
        assertThat(result.getId()).isEqualTo(1L);
        assertThat(result.getEmail()).isEqualTo(request.getEmail());
        assertThat(result.getUsername()).isEqualTo(request.getUsername());
        assertThat(result.getStatus()).isEqualTo(UserStatus.ACTIVE);
        
        verify(userRepository).existsByEmail(request.getEmail());
        verify(passwordEncoder).encode(request.getPassword());
        verify(userRepository).save(any(User.class));
    }
    
    @Test
    @DisplayName("Should throw exception when email already exists")
    void shouldThrowExceptionWhenEmailExists() {
        // Given
        CreateUserRequest request = CreateUserRequest.builder()
            .email("existing@example.com")
            .username("testuser")
            .password("password123")
            .build();
            
        when(userRepository.existsByEmail(request.getEmail())).thenReturn(true);
        
        // When & Then
        assertThatThrownBy(() -> userService.createUser(request))
            .isInstanceOf(DuplicateEmailException.class)
            .hasMessage("Email already exists: existing@example.com");
            
        verify(userRepository).existsByEmail(request.getEmail());
        verify(userRepository, never()).save(any(User.class));
    }
    
    // AI generates more test cases for edge cases
    @ParameterizedTest
    @ValueSource(strings = {"", " ", "invalid-email", "@example.com", "test@"})
    @DisplayName("Should validate email format")
    void shouldValidateEmailFormat(String invalidEmail) {
        CreateUserRequest request = CreateUserRequest.builder()
            .email(invalidEmail)
            .username("testuser")
            .password("password123")
            .build();
            
        assertThatThrownBy(() -> userService.createUser(request))
            .isInstanceOf(ValidationException.class);
    }
}
```

## Advanced AI Features

### 1. Code Refactoring

#### Legacy Code Modernization
```java
// Before (Legacy Java 8)
public class LegacyUserService {
    
    public List<User> getActiveUsers() {
        List<User> allUsers = userRepository.findAll();
        List<User> activeUsers = new ArrayList<>();
        for (User user : allUsers) {
            if (user.getStatus() == UserStatus.ACTIVE) {
                activeUsers.add(user);
            }
        }
        return activeUsers;
    }
}

// After (AI-suggested modern Java)
public class ModernUserService {
    
    public List<User> getActiveUsers() {
        return userRepository.findAll()
            .stream()
            .filter(user -> user.getStatus() == UserStatus.ACTIVE)
            .collect(Collectors.toList());
    }
    
    // Or even better with repository method
    public List<User> getActiveUsers() {
        return userRepository.findByStatus(UserStatus.ACTIVE);
    }
}
```

### 2. Design Pattern Implementation

#### AI-Generated Factory Pattern
```java
// AI Prompt: Implement Factory pattern for user creation
public abstract class UserFactory {
    
    public static User createUser(UserType type, CreateUserRequest request) {
        return switch (type) {
            case ADMIN -> createAdminUser(request);
            case CUSTOMER -> createCustomerUser(request);
            case EMPLOYEE -> createEmployeeUser(request);
            case GUEST -> createGuestUser(request);
        };
    }
    
    private static User createAdminUser(CreateUserRequest request) {
        User user = User.builder()
            .email(request.getEmail())
            .username(request.getUsername())
            .password(request.getPassword())
            .status(UserStatus.ACTIVE)
            .build();
        user.addRole(Role.ADMIN);
        user.addRole(Role.USER);
        return user;
    }
    
    private static User createCustomerUser(CreateUserRequest request) {
        User user = User.builder()
            .email(request.getEmail())
            .username(request.getUsername())
            .password(request.getPassword())
            .status(UserStatus.PENDING_VERIFICATION)
            .build();
        user.addRole(Role.CUSTOMER);
        return user;
    }
    
    // AI generates other factory methods...
}
```

### 3. Exception Handling

#### Global Exception Handler
```java
// AI generates comprehensive exception handling
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {
    
    @ExceptionHandler(UserNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ErrorResponse handleUserNotFound(UserNotFoundException ex, HttpServletRequest request) {
        log.warn("User not found: {}", ex.getMessage());
        return ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.NOT_FOUND.value())
            .error("User Not Found")
            .message(ex.getMessage())
            .path(request.getRequestURI())
            .build();
    }
    
    @ExceptionHandler(DuplicateEmailException.class)
    @ResponseStatus(HttpStatus.CONFLICT)
    public ErrorResponse handleDuplicateEmail(DuplicateEmailException ex, HttpServletRequest request) {
        log.warn("Duplicate email attempt: {}", ex.getMessage());
        return ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.CONFLICT.value())
            .error("Email Already Exists")
            .message(ex.getMessage())
            .path(request.getRequestURI())
            .build();
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public ErrorResponse handleValidationErrors(MethodArgumentNotValidException ex, HttpServletRequest request) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error ->
            errors.put(error.getField(), error.getDefaultMessage())
        );
        
        return ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.BAD_REQUEST.value())
            .error("Validation Failed")
            .message("Invalid input data")
            .validationErrors(errors)
            .path(request.getRequestURI())
            .build();
    }
}
```

## Configuration and Best Practices

### 1. AI Assistant Configuration
```json
{
  "ai.assistant.java.enableSmartCompletion": true,
  "ai.assistant.java.generateJavadoc": true,
  "ai.assistant.java.suggestRefactoring": true,
  "ai.assistant.spring.enableAnnotationHelp": true,
  "ai.assistant.testing.generateTestCases": true,
  "ai.assistant.performance.optimizationHints": true
}
```

### 2. Code Quality Integration
- Use AI for code review suggestions
- Generate comprehensive test coverage
- Identify potential security vulnerabilities
- Suggest performance optimizations
- Maintain coding standards consistency

### 3. Documentation Generation
```java
/**
 * AI-generated comprehensive Javadoc
 * 
 * Service class for managing user operations including CRUD operations,
 * authentication, and user status management.
 * 
 * This service provides transactional operations for user management
 * with proper error handling and validation.
 * 
 * @author AI Assistant
 * @version 1.0
 * @since 2024-01-01
 * 
 * @see User
 * @see UserRepository
 * @see UserStatus
 */
@Service
@Transactional
public class UserService {
    // Implementation...
}
```

## Troubleshooting

### Common Issues
1. **AI suggestions not working**: Check plugin activation and internet connection
2. **Slow response time**: Adjust AI model settings and IDE memory allocation
3. **Irrelevant suggestions**: Provide better context and use descriptive names
4. **Integration errors**: Verify Spring Boot version compatibility

### Performance Optimization
- Configure AI cache settings
- Limit background AI processing
- Use local models when possible
- Optimize suggestion frequency

## Conclusion

IntelliJ IDEA with AI integration transforms Java development by providing intelligent code generation, automated refactoring, and comprehensive testing support. The combination of AI tools with IntelliJ's powerful features creates an exceptionally productive development environment for modern Java applications. 