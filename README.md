# How to create an Azure Java Function Http Triggered using IntelliJ

Install IntelliJ Community Edition: https://www.jetbrains.com/idea/download/?section=windows

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/e6a2ac02-bef0-4756-bba2-f1ad21fabab5)

Run IntelliJ Community Edition

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/c46f9f98-101c-432d-97bd-5f74ad0e38fa)

Install "**Azure Toolkit for IngelligJ**" plugin

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/d9bdeb67-925f-4a77-92a1-f55391154e72)

Create a new project

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/b6052ef5-5d00-42a9-aa07-4850902a77e6)

Select "Azure Functions", Function trigger "HttpTrigger", project SDK "Oracle openJDK version 20.0.1": 

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/220f1e2f-3784-4069-8ecd-3f8bd69a41da)

Select project manager tool "Maven", group name "com.example", artifact "azure-function-examples", version "1.0.0-SNAPSHOT", package name "org.example.functions":

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/171f1b99-35fb-45fc-a4c2-f129afa7f1a7)

Also set the project name "azure-function-examples" and project location "C:\\azure-function-examples":

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/e0432c12-b6f4-45f5-95f1-5359255c2842)

To avoid any problem with the Antivirus configure Microsoft Defender automatically:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/5623fd13-7c09-4fb9-8fc9-eadd41ab8a93)

This is the project structure:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/e0d8ad65-6480-40a5-b07a-ea2417857a2e)

This is the Azure Java Function source code:

```java
package org.example.functions;

import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;

/**
 * Azure Functions with HTTP Trigger.
 */
public class HttpTriggerJava {
    /**
     * This function listens at endpoint "/api/HttpTriggerJava". Two ways to invoke it using "curl" command in bash:
     * 1. curl -d "HTTP Body" {your host}/api/HttpTriggerJava
     * 2. curl {your host}/api/HttpTriggerJava?name=HTTP%20Query
     */
    @FunctionName("HttpTriggerJava")
    public HttpResponseMessage run(
            @HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION) HttpRequestMessage<Optional<String>> request,
            final ExecutionContext context) {
        context.getLogger().info("Java HTTP trigger processed a request.");

        // Parse query parameter
        String query = request.getQueryParameters().get("name");
        String name = request.getBody().orElse(query);

        if (name == null) {
            return request.createResponseBuilder(HttpStatus.BAD_REQUEST).body("Please pass a name on the query string or in the request body").build();
        } else {
            return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
        }
    }
}
```

Run the application: 

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/bd78ff90-3697-49a7-b7d9-c07f4a3725c4)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/a87430d1-9bb7-4c87-84b1-d44488ce5d0e)

See the application output:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/9d2f18ad-ae42-4e16-b258-3c594504d540)



