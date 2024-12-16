# API-Testing-RestAssured-GitHub-Actions  

This repository demonstrates API testing using [RestAssured](https://rest-assured.io/) integrated with GitHub Actions for continuous integration and automated test execution.  

## Features  
- API testing with RestAssured in Java  
- Automated CI pipeline using GitHub Actions  
- Test reports generation and integration  
- Data-driven testing for dynamic API validations  

## Prerequisites  
- Java (JDK 8 or higher)  
- Maven  
- GitHub repository  

## Getting Started  

1. **Clone the repository**:  
   ```bash  
   git clone https://github.com/Razib-R75/API-testing-using-restassured-github-actions/edit/main 
   cd API-Testing-RestAssured-GitHub-Actions  
   ```  

2. **Install dependencies**:  
   Run the following command to download all dependencies:  
   ```bash  
   mvn clean install  
   ```  

3. **Run tests locally**:  
   Execute the tests using Maven:  
   ```bash  
   mvn test  
   ```  

4. **Automated CI with GitHub Actions**:  
   Push changes to your GitHub repository to trigger the automated pipeline.  
   GitHub Actions will:  
   - Build the project  
   - Execute API tests  
   - Generate reports  

## Example Test Case  
```java  
import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.equalTo;

public class APITest {

    @Test
    public void testGetRequest() {
        RestAssured.baseURI = "https://jsonplaceholder.typicode.com";
        
        given()
            .when()
            .get("/posts/1")
            .then()
            .statusCode(200)
            .body("id", equalTo(1))
            .body("title", equalTo("sunt aut facere repellat provident occaecati excepturi optio reprehenderit"));
    }
}
```  

## GitHub Actions Configuration  
The repository includes a pre-configured `github/workflows/ci.yml` file to automate testing.  

Example `ci.yml`:  
```yaml  
name: API Testing CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up JDK
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'adopt'

    - name: Install dependencies
      run: mvn install

    - name: Run API tests
      run: mvn test
```  

## Resources  
- [RestAssured Documentation](https://rest-assured.io/)  
- [GitHub Actions Documentation](https://docs.github.com/en/actions)  

## Contributing  
Contributions are welcome! Feel free to submit issues or pull requests to improve the examples or add new features.  

