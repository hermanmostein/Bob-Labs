# Lab 5: Java Application Modernization with Bob

## Overview

In this lab, you'll learn how to use Bob to modernize legacy Java applications, upgrading from Java 8 to Java 17/21 while leveraging modern language features, improving performance, and maintaining backward compatibility. This lab demonstrates Bob's capabilities in understanding complex codebases and applying systematic modernization patterns.

> **☕ Bob Differentiator: [Enterprise Java Modernization](../bob-differentiators.md#4--enterprise-java-modernization)**
> Bob uniquely integrates with IBM's Application Modernization Accelerator to deeply understand and modernize Java applications. Unlike generic AI assistants, Bob can comprehend complex J2EE patterns, automatically migrate to Liberty, upgrade Java versions, and apply modern patterns—all while maintaining business logic integrity. This is one of Bob's most powerful differentiators for enterprise development teams.

**Duration:** 75-90 minutes (may take longer if Bob experiences service issues)
**Difficulty:** Advanced
**Prerequisites:** Completion of Labs 1-4, Java development experience

## Learning Objectives

By the end of this lab, you will be able to:

1. Analyze legacy Java code and identify modernization opportunities
2. Use Bob to upgrade Java 8 code to Java 17/21
3. Leverage modern Java features (records, sealed classes, pattern matching, etc.)
4. Migrate from legacy APIs to modern alternatives
5. Improve performance with modern JVM features
6. Maintain backward compatibility during migration
7. Create comprehensive migration documentation

## 💡 Lab Approach

This lab uses Bob's **UI interface**  to provide an interactive, visual learning experience:

- **🖥️ UI Approach Benefits**:
  - More interactive and visual
  - Better for learning and understanding Bob's capabilities
  - Easier to review changes before applying
  - Great for complex refactoring with multiple steps
  - Provides immediate feedback and explanations
  - Perfect for understanding the modernization process step-by-step

**Note:** For command-line automation approaches, refer to [Lab 4](../lab4/README.md) which covers BobShell in detail.

## What You'll Modernize

This lab focuses on modernizing a legacy Java 8 e-commerce application to Java 17/21, including:

- **Language Features**: Upgrade to records, sealed classes, pattern matching, switch expressions
- **API Modernization**: Migrate from Date to java.time, Collections improvements
- **Concurrency**: Update to modern concurrency utilities and virtual threads
- **Performance**: Leverage JVM improvements and modern garbage collectors
- **Dependencies**: Update libraries and frameworks to modern versions

## Lab Structure

```
lab5/
├── README.md                           # This file
├── legacy/                             # Java 8 legacy code
│   ├── src/
│   │   └── main/
│   │       └── java/
│   │           └── com/example/ecommerce/
│   │               ├── model/          # Domain models
│   │               ├── service/        # Business logic
│   │               ├── repository/     # Data access
│   │               └── util/           # Utilities
│   ├── pom.xml                         # Maven configuration (Java 8)
│   └── README.md                       # Legacy code documentation
├── modernized/                         # Java 17/21 modernized code
│   ├── src/
│   │   └── main/
│   │       └── java/
│   │           └── com/example/ecommerce/
│   │               ├── model/          # Modern domain models
│   │               ├── service/        # Modernized business logic
│   │               ├── repository/     # Updated data access
│   │               └── util/           # Modern utilities
│   ├── pom.xml                         # Maven configuration (Java 17/21)
│   └── README.md                       # Modernized code documentation
└── migration-guide/                    # Migration documentation
    ├── analysis-report.md              # Initial analysis
    ├── migration-plan.md               # Step-by-step plan
    ├── feature-comparison.md           # Before/after comparison
    └── best-practices.md               # Modernization best practices
```

## Part 1: Analyzing Legacy Code

### Step 1.1: Understanding the Legacy Application

First, let's examine the legacy Java 8 application structure:

**Legacy Application Components:**
- Product management system
- Order processing
- User authentication
- Payment processing
- Inventory management

The application uses:
- Java 8 language features
- Legacy Date/Calendar APIs
- Traditional exception handling
- Verbose null checks
- Anonymous inner classes
- Legacy collection operations

### Step 1.2: Initial Analysis with Bob

Analyze the legacy codebase using Bob's UI:

1. **Open Bob in your IDE**
   - Launch Bob from your IDE's sidebar or command palette
   - Ensure you're in **Plan Mode** (📝 Plan mode)

2. **Add the Legacy Code to Context**
   - In the Bob chat input field, type `@` to open the file navigator
   - Browse to `lab5/legacy/src/` and select the Java files you want to analyze
   - You can select multiple files by typing `@` again for each file
   - Bob will load the selected files into the conversation context
   - **Note:** Adding files with `@` gives Bob context to analyze them, but doesn't open them in your editor

3. **Request Analysis**
   In the Bob chat interface, type:
   ```
   Analyze this Java 8 codebase and identify modernization opportunities for upgrading to Java 17.
   Focus on:
   - Opportunities to use records instead of POJOs
   - Places to apply pattern matching
   - Code that can use switch expressions
   - Areas where Optional can replace null checks
   - Streams that can be simplified
   - Date/Time API migration opportunities
   
   Create a detailed analysis report and save it to migration-guide/analysis-report.md
   ```

4. **Review Bob's Analysis**
   Bob will provide:
   - Complexity metrics and maintainability scores
   - Specific modernization opportunities with code examples
   - Breaking changes to watch for
   - Expected performance improvements
   - Estimated migration effort

5. **Bob Will Auto-Save the Analysis**
   - Bob will automatically create and save the markdown file to `migration-guide/analysis-report.md`
   - You don't need to manually save the response
   - If Bob doesn't save automatically, explicitly ask: "Please save this analysis to migration-guide/analysis-report.md"

> **💡 Tip: Working Within a Single Task**
> You can complete this entire lab within one continuous Bob conversation. When Bob finishes a step, simply provide your next instruction in the same chat. The blue "New Task" button appears when Bob is idle, but you only need to use it if you want to start a completely fresh conversation with no prior context.

**What Bob Identifies:**
- Opportunities to use records instead of POJOs
- Places to apply pattern matching
- Code that can use switch expressions
- Areas where Optional can replace null checks
- Streams that can be simplified
- Date/Time API migration opportunities

### Step 1.3: Review Analysis Report

Open the generated analysis report to understand:

1. **Complexity Metrics**: Current code complexity and maintainability
2. **Modernization Opportunities**: Specific features that can be upgraded
3. **Breaking Changes**: Potential compatibility issues
4. **Performance Improvements**: Expected performance gains
5. **Migration Effort**: Estimated time and complexity

## Part 2: Creating Migration Plan

### Step 2.1: Generate Migration Plan with Bob

1. **Stay in Plan Mode** (📝 Plan mode) or switch to it if needed

2. **Ensure Legacy Code is in Context**
   - If continuing from Step 1.2, the files should still be in Bob's context
   - If starting fresh, type `@` in the chat input to add the legacy Java files
   - Add the analysis report by typing `@migration-guide/analysis-report.md`

3. **Request Migration Plan**
   In Bob's chat interface, type:
   ```
   Create a detailed migration plan for upgrading this Java 8 application to Java 17, including:
   - Phase-by-phase approach
   - Risk assessment
   - Testing strategy
   - Rollback procedures
   - Timeline estimates
   
   Base this on @migration-guide/analysis-report.md and save the plan to migration-guide/migration-plan.md
   ```

4. **Bob Will Create the Migration Plan**
   - Bob will generate a detailed, phased migration plan
   - Bob will automatically save it to `migration-guide/migration-plan.md`
   - Review the plan and ask Bob to make adjustments if needed

**Migration Plan Phases:**

1. **Phase 1: Preparation**
   - Update build tools (Maven/Gradle)
   - Update dependencies
   - Set up Java 17 environment
   - Create feature branches

2. **Phase 2: Language Features**
   - Convert POJOs to records
   - Apply pattern matching
   - Use switch expressions
   - Implement sealed classes

3. **Phase 3: API Modernization**
   - Migrate Date/Calendar to java.time
   - Update Collections usage
   - Modernize Stream operations
   - Update concurrency utilities

4. **Phase 4: Performance Optimization**
   - Leverage JVM improvements
   - Update garbage collector settings
   - Optimize memory usage
   - Profile and benchmark

5. **Phase 5: Testing & Validation**
   - Run comprehensive tests
   - Performance testing
   - Security validation
   - User acceptance testing

### Step 2.2: Risk Assessment

**Common Risks to Consider:**
- Removed APIs (e.g., Java EE modules)
- Changed behavior in APIs
- Dependency compatibility
- Performance regressions
- Security implications

## Part 3: Modernizing Domain Models

### Step 3.1: Convert POJOs to Records

Let's modernize the domain models using Bob:

**Legacy Product.java (Java 8):**
```java
public class Product {
    private final String id;
    private final String name;
    private final BigDecimal price;
    private final String category;
    
    public Product(String id, String name, BigDecimal price, String category) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.category = category;
    }
    
    // Getters, equals, hashCode, toString...
    // 50+ lines of boilerplate code
}
```

1. **Switch to Code Mode** (💻 Code mode)

2. **Add the Legacy File to Context**
   - Type `@lab5/legacy/src/main/java/com/example/ecommerce/model/Product.java` to add it to Bob's context
   - Alternatively, open the file in your editor and it will be automatically added to context

3. **Request Modernization**
   In Bob's chat, type:
   ```
   Convert this Product class to a Java 17 record. Include:
   - Compact constructor for validation
   - Null checks for required fields
   - Validation for price (must be non-negative)
   - Proper JavaDoc comments
   
   Save the modernized version to lab5/modernized/src/main/java/com/example/ecommerce/model/Product.java
   ```

4. **Review and Apply**
   - Bob will show you the modernized code
   - Review the changes carefully
   - Bob will automatically create the file in the modernized directory
   - Confirm the changes were applied successfully before proceeding

**Modernized Product.java (Java 17):**
```java
public record Product(
    String id,
    String name,
    BigDecimal price,
    String category
) {
    // Compact constructor for validation
    public Product {
        Objects.requireNonNull(id, "Product ID cannot be null");
        Objects.requireNonNull(name, "Product name cannot be null");
        if (price.compareTo(BigDecimal.ZERO) < 0) {
            throw new IllegalArgumentException("Price cannot be negative");
        }
    }
}
```

**Benefits:**
- Reduced from 50+ lines to ~15 lines
- Immutable by default
- Built-in equals, hashCode, toString
- Better performance
- More readable

### Step 3.2: Implement Sealed Classes

Use sealed classes for type hierarchies. In Bob's UI, request modernization of the Payment class hierarchy to use sealed classes.

Open Payment.java, and in Bob's chat, type:
```
Modernize this Payment class to use sealed classes.
```

**Before (Java 8):**
```java
public abstract class Payment {
    protected BigDecimal amount;
    // ...
}

public class CreditCardPayment extends Payment { }
public class PayPalPayment extends Payment { }
public class BankTransferPayment extends Payment { }
```

**After (Java 17):**
```java
public sealed interface Payment permits CreditCardPayment, PayPalPayment, BankTransferPayment {
    BigDecimal amount();
    PaymentStatus process();
}

public record CreditCardPayment(
    BigDecimal amount,
    String cardNumber,
    String cvv,
    LocalDate expiryDate
) implements Payment {
    @Override
    public PaymentStatus process() {
        // Implementation
    }
}

// Similar for other payment types
```

## Part 4: Modernizing Business Logic

### Step 4.1: Pattern Matching and Switch Expressions

Modernize conditional logic:

1. **Open PaymentService.java**
   - Navigate to `lab5/legacy/src/main/java/com/example/ecommerce/service/PaymentService.java`
   - Ensure you're in **Code Mode** (💻)

2. **Select the Method to Modernize**
   - Highlight the `calculateFee` method (or the entire class)
   - Right-click and select "IBM Bob" -> "Add to Context".

3. **Request Modernization**
   ```
   Modernize this payment fee calculation method to use Java 17 features:
   - Replace instanceof checks with pattern matching
   - Use switch expressions instead of if-else chains
   - Make the code more concise and readable
   - Ensure exhaustiveness checking with sealed classes
   
   Show me the before and after comparison.
   ```

4. **Review and Apply**
   - Bob will show the modernized code with pattern matching
   - Review the improvements
   - Apply the changes when satisfied

**Before (Java 8):**
```java
public BigDecimal calculateFee(Payment payment) {
    if (payment instanceof CreditCardPayment) {
        CreditCardPayment cc = (CreditCardPayment) payment;
        return cc.getAmount().multiply(new BigDecimal("0.029"));
    } else if (payment instanceof PayPalPayment) {
        PayPalPayment pp = (PayPalPayment) payment;
        return pp.getAmount().multiply(new BigDecimal("0.034"));
    } else if (payment instanceof BankTransferPayment) {
        return BigDecimal.ZERO;
    } else {
        throw new IllegalArgumentException("Unknown payment type");
    }
}
```

**After (Java 17):**
```java
public BigDecimal calculateFee(Payment payment) {
    return switch (payment) {
        case CreditCardPayment cc -> cc.amount().multiply(new BigDecimal("0.029"));
        case PayPalPayment pp -> pp.amount().multiply(new BigDecimal("0.034"));
        case BankTransferPayment bt -> BigDecimal.ZERO;
    };
}
```

### Step 4.2: Stream API Improvements

Modernize collection operations using Bob's UI:

1. **Open OrderService.java**
2. **Request Stream Optimization** in Bob's chat:
   ```
   Modernize the stream operations in this code to use Java 17 improvements:
   - Replace .collect(Collectors.toList()) with .toList()
   - Optimize stream pipelines
   - Use modern collection factory methods
   ```

**Before (Java 8):**
```java
public List<Order> findHighValueOrders(List<Order> orders) {
    return orders.stream()
        .filter(order -> order.getTotal().compareTo(new BigDecimal("1000")) > 0)
        .collect(Collectors.toList());
}
```

**After (Java 17):**
```java
public List<Order> findHighValueOrders(List<Order> orders) {
    return orders.stream()
        .filter(order -> order.total().compareTo(new BigDecimal("1000")) > 0)
        .toList();  // Simpler, returns immutable list
}
```

## Part 5: API Modernization

### Step 5.1: Date/Time API Migration

Migrate from legacy Date/Calendar to java.time using Bob's UI:

1. **Identify Date/Time Usage** in your codebase
2. **Request Migration** in Bob's chat:
   ```
   Migrate all Date and Calendar usage to java.time API:
   - Replace Date with LocalDateTime or Instant
   - Replace Calendar with LocalDateTime
   - Update date comparison logic
   - Modernize date formatting
   ```

**Before (Java 8):**
```java
public class Order {
    private Date orderDate;
    private Date deliveryDate;
    
    public boolean isOverdue() {
        Calendar cal = Calendar.getInstance();
        cal.setTime(deliveryDate);
        return cal.before(Calendar.getInstance());
    }
}
```

**After (Java 17):**
```java
public record Order(
    String id,
    LocalDateTime orderDate,
    LocalDateTime deliveryDate,
    // ... other fields
) {
    public boolean isOverdue() {
        return deliveryDate.isBefore(LocalDateTime.now());
    }
}
```

### Step 5.2: Optional Usage

Replace null checks with Optional using Bob's UI:

1. **Open repository or service files** with null checks
2. **Request Optional Introduction** in Bob's chat:
   ```
   Refactor this code to use Optional instead of null checks:
   - Replace null returns with Optional
   - Use Optional methods (ifPresent, orElse, etc.)
   - Improve null safety
   ```

**Before (Java 8):**
```java
public Product findById(String id) {
    Product product = database.get(id);
    if (product == null) {
        throw new ProductNotFoundException(id);
    }
    return product;
}
```

**After (Java 17):**
```java
public Optional<Product> findById(String id) {
    return Optional.ofNullable(database.get(id));
}

// Usage
productRepository.findById(id)
    .ifPresentOrElse(
        product -> processProduct(product),
        () -> handleNotFound(id)
    );
```

## Part 6: Concurrency Modernization

### Step 6.1: Virtual Threads (Java 21)

If targeting Java 21, leverage virtual threads using Bob's UI:

1. **Open AsyncService.java** with ExecutorService usage
2. **Request Virtual Threads Migration** in Bob's chat:
   ```
   Modernize this code to use Java 21 virtual threads:
   - Replace fixed thread pools with virtual thread executors
   - Update ExecutorService creation
   - Optimize for virtual thread usage
   ```

**Before (Java 8):**
```java
ExecutorService executor = Executors.newFixedThreadPool(100);

public void processOrders(List<Order> orders) {
    for (Order order : orders) {
        executor.submit(() -> processOrder(order));
    }
}
```

**After (Java 21):**
```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();

public void processOrders(List<Order> orders) {
    orders.forEach(order -> 
        executor.submit(() -> processOrder(order))
    );
}
```

### Step 6.2: CompletableFuture Improvements

Modernize async operations using Bob's UI:

1. **Open AsyncService.java**
2. **Request Async Modernization** in Bob's chat:
   ```
   Modernize the CompletableFuture usage in this code:
   - Use modern async patterns
   - Improve error handling
   - Optimize async chains
   ```

## Part 7: Dependency Updates

### Step 7.1: Update Maven Configuration

Use Bob's UI to update pom.xml:

1. **Open pom.xml** in your editor
2. **Request Maven Update** in Bob's chat:
   ```
   Update this pom.xml for Java 17:
   - Change compiler source and target to 17
   - Add compiler release property
   - Update Spring and other dependencies to Java 17 compatible versions
   - Save to lab5/modernized/pom.xml
   ```

**Before (Java 8 pom.xml):**
```xml
<properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring.version>5.3.20</spring.version>
</properties>
```

**After (Java 17 pom.xml):**
```xml
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <maven.compiler.release>17</maven.compiler.release>
    <spring.version>6.0.11</spring.version>
</properties>
```

### Step 7.2: Dependency Compatibility Check

Check all dependencies for Java 17 compatibility using Bob's UI:

1. **Switch to Plan Mode** (📝)
2. **Open pom.xml** and add to context with `@`
3. **Request Compatibility Analysis** in Bob's chat:
   ```
   Analyze this pom.xml for Java 17 compatibility:
   - Identify dependencies that need updates
   - Suggest Java 17 compatible versions
   - Flag any incompatible dependencies
   - Recommend alternatives if needed
   
   Save the analysis to lab5/migration-guide/dependency-report.md
   ```

## Part 8: Testing and Validation

### Step 8.1: Generate Migration Tests

Create tests to validate the migration using Bob's UI:

1. **Switch to Code Mode** (💻)
2. **Request Test Generation** in Bob's chat:
   ```
   Create comprehensive tests to validate the Java 8 to Java 17 migration:
   - Functional equivalence tests
   - Performance comparison tests
   - API compatibility tests
   - Integration tests
   
   Compare behavior between legacy/ and modernized/ code.
   Save to lab5/modernized/src/test/java/MigrationValidationTest.java
   ```

### Step 8.2: Performance Benchmarking

Compare performance before and after using Bob's UI:

1. **Request Benchmark Generation** in Bob's chat:
   ```
   Create JMH benchmarks to compare performance between Java 8 and Java 17:
   - Record creation vs POJO
   - Pattern matching vs instanceof
   - Stream operations
   - Date/Time operations
   
   Save to lab5/modernized/src/test/java/PerformanceBenchmark.java
   ```

## Part 9: Documentation Generation

### Step 9.1: Generate Migration Documentation

Create comprehensive documentation using Bob's UI:

1. **Switch to Plan Mode** (📝)
2. **Request Feature Comparison** in Bob's chat:
   ```
   Create a detailed comparison document showing:
   - Side-by-side code examples (Java 8 vs Java 17)
   - Performance improvements
   - Code reduction metrics
   - Maintainability improvements
   
   Analyze both legacy/ and modernized/ directories.
   Save to lab5/migration-guide/feature-comparison.md
   ```

3. **Request Best Practices Guide**:
   ```
   Create a best practices guide for Java modernization:
   - When to use records vs classes
   - Sealed class usage patterns
   - Pattern matching best practices
   - Stream API optimization
   - Concurrency patterns
   
   Save to lab5/migration-guide/best-practices.md
   ```

> **📝 Note: Bob's Documentation Generation**
> Bob may create additional markdown files during the lab (such as `JAVADOC_GENERATION_GUIDE.md` or similar) to provide supplementary guidance. These are helpful reference materials that Bob generates to support your learning. You can keep them for reference or remove them if not needed.

### Step 9.2: Generate API Documentation

Update API documentation for the modernized code using Bob's UI:

1. **Request JavaDoc Generation** in Bob's chat:
   ```
   Generate comprehensive JavaDoc documentation for the modernized code in lab5/modernized/src/:
   - Include all public APIs
   - Document Java 17 features used
   - Add usage examples
   - Format as HTML
   
   Save to lab5/modernized/docs/api/
   ```

2. **Request Architecture Documentation**:
   ```
   Generate architecture documentation for the modernized application:
   - System overview
   - Component relationships
   - Design patterns used
   - Java 17 features utilized
   
   Save to lab5/modernized/docs/architecture.md
   ```

## Part 10: Deployment and Rollout

### Step 10.1: Create Deployment Plan

Generate a deployment strategy using Bob's UI:

1. **Switch to Plan Mode** (📝)
2. **Request Deployment Plan** in Bob's chat:
   ```
   Create a deployment plan for rolling out the Java 17 modernized application:
   - Blue-green deployment strategy
   - Rollback procedures
   - Monitoring and alerting
   - Performance validation
   - Gradual rollout phases
   
   Save to lab5/migration-guide/deployment-plan.md
   ```

### Step 10.2: Create Rollback Procedures

Ensure you can rollback if needed using Bob's UI:

1. **Request Rollback Guide** in Bob's chat:
   ```
   Create detailed rollback procedures:
   - When to rollback
   - Rollback steps
   - Data migration rollback
   - Validation after rollback
   - Communication plan
   
   Save to lab5/migration-guide/rollback-procedures.md
   ```

## Exercises

### Exercise 1: Modernize Additional Classes

Use Bob to modernize these additional classes:
1. `Customer.java` - Convert to record with validation
2. `OrderStatus.java` - Convert to sealed interface
3. `InventoryService.java` - Apply pattern matching

### Exercise 2: Performance Analysis

1. Run performance benchmarks
2. Compare memory usage
3. Analyze GC behavior
4. Document improvements

### Exercise 3: Create Migration Checklist

Generate a comprehensive checklist for future migrations using Bob's UI:
```
Create a reusable checklist for Java modernization projects including all key steps and considerations.
```

## Best Practices

### 1. Incremental Migration

- Migrate one module at a time
- Maintain backward compatibility
- Test thoroughly at each step
- Use feature flags for gradual rollout

### 2. Maintain Compatibility

- Keep interfaces stable
- Use @Deprecated for old APIs
- Provide migration guides
- Version your APIs

### 3. Performance Validation

- Benchmark before and after
- Monitor production metrics
- Profile memory usage
- Test under load

### 4. Documentation

- Document all changes
- Explain why changes were made
- Provide migration examples
- Update team knowledge base

## Common Pitfalls

### 1. Breaking Changes

**Issue**: Removed APIs in newer Java versions
**Solution**: Use Bob to identify and suggest alternatives

### 2. Dependency Conflicts

**Issue**: Libraries not compatible with Java 17
**Solution**: Update dependencies or find alternatives

### 3. Performance Regressions

**Issue**: Unexpected performance decrease
**Solution**: Profile and benchmark, adjust GC settings

### 4. Over-Modernization

**Issue**: Changing too much at once
**Solution**: Incremental approach, focus on high-value changes

## Summary

In this lab, you learned:

✅ How to analyze legacy Java code for modernization opportunities
✅ Using Bob to upgrade Java 8 code to Java 17/21
✅ Leveraging modern Java features (records, sealed classes, pattern matching)
✅ Migrating from legacy APIs to modern alternatives
✅ Improving performance with modern JVM features
✅ Creating comprehensive migration documentation
✅ Testing and validating migrations
✅ Deploying modernized applications safely

> **🎯 Bob's Java Modernization Advantage**
> You've experienced Bob's unique [Enterprise Java Modernization](../bob-differentiators.md#4--enterprise-java-modernization) capabilities. Bob can handle complex J2EE to Liberty migrations, understand legacy business logic, and apply modern patterns systematically. This deep Java expertise, combined with IBM's modernization tools, makes Bob uniquely valuable for enterprise Java teams. While Bob excels at Java, these modernization techniques can also be applied to other languages like Python, JavaScript, .NET, and more.

## Next Steps

- **Lab 6**: Learn how to create custom MCP servers and modes
- Apply these techniques to your own Java projects
- Explore Java 21 features (virtual threads, structured concurrency)
- Share your modernization experiences with the team

## Additional Resources

- [Java 17 Migration Guide](https://docs.oracle.com/en/java/javase/17/migrate/)
- [Java 21 Features](https://openjdk.org/projects/jdk/21/)
- [Modern Java Patterns](https://www.oracle.com/java/technologies/javase/17-relnote-issues.html)
- [Bob Java Modernization Guide](https://ibm.com/bob/docs/java-modernization)

---

**Need Help?** If you encounter issues:
1. Check the migration guide documentation
2. Review the analysis reports
3. Consult the best practices guide
4. Ask in the Bob community forums

**Feedback:** Help us improve this lab by providing feedback on what worked well and what could be better!
