# Dynamic creation of Redux Types and action creators

Here is the following function which takes takes two parameters
1 first parameter is the object which contains the list of your types or action creations
2 second is the returned object which is object used to returned by the action creation function.

let's have a look at the Action creator


        // this function takes the args and return the new created function with the same arguments.
        function generate (args) {
          return function (...args) {
          }
        }
   
        
       // Action creatior with two arguments 
       
        function createActions(properties, values) {
        values.Types = {};
        values.Actions = {}
              for (let i in properties) {
                let types = i.toUpperCase();
                values.Types[types] = types
                values.Actions[types] = generate(properties[i])
              }
              return values;
        }
        
        
        const  {Types, Actions } = createActions({
          loginRequest: ['username', 'password'],
          userDetails: ['id'],
          loginFailure: ['error'],
          requestWithDefaultValues: { username: 'guest', password: null },
          custom: (a, b) => ({ type: 'CUSTOM', total: a + b })
        }, {})
        
        console.log(Types) // {LOGINREQUEST: "LOGINREQUEST", USERDETAILS: "USERDETAILS", LOGINFAILURE: "LOGINFAILURE", REQUESTWITHDEFAULTVALUES: "REQUESTWITHDEFAULTVALUES", CUSTOM: "CUSTOM"}
LOGINREQUEST: "LOGINREQUEST"
USERDETAILS: "USERDETAILS"
LOGINFAILURE: "LOGINFAILURE"
REQUESTWITHDEFAULTVALUES: "REQUESTWITHDEFAULTVALUES"
CUSTOM: "CUSTOM"
__proto__: Object



        console.log(Actions) // {LOGINREQUEST: ƒ, USERDETAILS: ƒ, LOGINFAILURE: ƒ, REQUESTWITHDEFAULTVALUES: ƒ, CUSTOM: ƒ}LOGINREQUEST: ƒ (...args)USERDETAILS: ƒ (...args)LOGINFAILURE: ƒ (...args)REQUESTWITHDEFAULTVALUES: ƒ (...args)CUSTOM: ƒ (...args)__proto__: Object






