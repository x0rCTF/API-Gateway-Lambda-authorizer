```node
exports.handler =  function(event, context, callback) {

    // Token validation //
    const t1 = "t0keniz3d";             // API KEY //                 
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
