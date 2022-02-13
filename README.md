# Lambda Authorizer Function
![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fx0rCTF%2FAPI-Gateway-Lambda-authorizer&countColor=%23263759&style=plastic)

```node
exports.handler =  function(event, context, callback) {

    // Token validation //
    const t1 = "t0keniz3d";                      
    const t2 = event.authorizationToken;
    const methodArn = event.methodArn
    if (t1 === t2) {
        callback(null, generatePolicy('user', 'Allow', methodArn));    
    } else {
        callback(null, generatePolicy('user', 'Deny', methodArn));      
    }
};

    // Construct //
var generatePolicy = function(principalId, effect, resource) {
    var authResponse = {};
    
    authResponse.principalId = principalId;
    if (effect && resource) {
        var policyDocument = {};
        policyDocument.Version = '2012-10-17'; 
        policyDocument.Statement = [];
        var statementOne = {};
        statementOne.Action = 'execute-api:Invoke'; 
        statementOne.Effect = effect;
        statementOne.Resource = resource;
        policyDocument.Statement[0] = statementOne;
        authResponse.policyDocument = policyDocument;
    };
    
    // Return //
    return authResponse;
}
```
# Requests:
## 401 Unauthorized
[![](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/401-Unauthorized.jpg)](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/401-Unauthorized.jpg)

## 403 Forbidden
[![](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/403-Forbidden.jpg)](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/403-Forbidden.jpg)

## 200 OK
[![](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/200-OK.jpg)](https://github.com/x0rCTF/API-Gateway-Lambda-authorizer/blob/main/images/200-OK.jpg)
