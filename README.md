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

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/66e30920-41ca-45b4-b0b4-d901f5947db1)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/e32ddd5e-9f61-4f3b-8363-5dc38e308b44)

See the application output:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/80e4c1e1-26e0-44d6-8789-96e1e6c1b499)

We input the Azure Function endpoint URL in the internet web browser:

http://localhost:54658/api/HttpTriggerJava

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/f9543a97-507f-4427-9de4-f9f895040379)

Also we can set the "name" parameter as a querystring in the above URL:

http://localhost:54658/api/HttpTriggerJava?name="my name is John"

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/90ced6d9-0dd2-4159-841e-c5fa4e845706)

Before deploying the Azure Java Function in the Azure Portal we can the deployment region "westeurope" in the pom.xml file:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/1df71225-744d-41ca-9793-324d0ba02748)

We deploy the application clicking on the "Deploy to Azure..." link:

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/16bd645a-b47e-402c-920c-cf239be5c360)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/4676085e-3aae-4f70-88c7-4960699d6329)

If you previously created a Function in Azure Portal then select it, otherwise we create a new Function in Azure portal to host our application 

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/97cd3108-825c-471c-8f18-242b23854a41)

When the deployment is finished you can Login in Azure Portal and inside the Azure Functions list we select our new Function

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/5bfac552-5864-463c-b268-6e5f22cb2fab)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/a832260c-8c54-44ee-9f10-eaa61a57c885)

We click on the button "Get Function Url" to copy the Azure Function URL: 

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/28bd97cb-4dcc-4390-bd95-7d2b2c8a4954)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/cc5c900d-eef1-4f27-815f-9c70cdefbb5b)

![image](https://github.com/luiscoco/Azure_Java_Function_Http_Triggered_using_IntelliJ/assets/32194879/92f970ae-06c3-4df9-9b30-1a049e9a10b7)



