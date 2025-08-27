# Refactor Test

Refactor test files to match updated service/class implementations.

---

I need to refactor a test file to match an updated service implementation. Please analyze both files and update the test accordingly.

Test file: {{arg1:test_file_path}}
Service file: {{arg2:service_file_path}}

Please:

1. **Read and analyze the service file** to understand:
   - Current method signatures and parameters
   - Dependencies and injected services  
   - Public methods that need testing
   - Any enum or constant dependencies
   - Exception handling patterns

2. **Read the existing test file** to understand:
   - Current test structure
   - Existing mock dependencies
   - Test data setup
   - Current assertions and test cases

3. **Refactor the test file** to:
   - Remove obsolete test methods for deleted service methods
   - Update test methods for changed method signatures
   - Add/remove @Mock dependencies as needed
   - Update test data setup to match new requirements
   - Add new test methods for any new public methods
   - Ensure proper error case testing
   - Maintain existing test logic where still applicable

4. **Focus on**:
   - Updating @Mock annotations and dependencies
   - Fixing method calls with new parameters
   - Updating assertions to match new return types
   - Adding tests for new functionality
   - Removing tests for removed functionality
   - Following Java testing best practices (JUnit 5, Mockito)

If the service file path is not provided, try to infer it from the test file path by:
- Replacing `/test/` with `/main/` in the path
- Removing `Test` from the class name

Keep the test comprehensive and ensure all public methods are properly tested.