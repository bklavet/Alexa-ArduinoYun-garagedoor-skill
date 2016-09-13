var http = require('http'); // if going through a proxy that uses SSL change to "require('https');"


////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
var local_ip = 'nearbus.net';

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
 * App ID for the skill
 */
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
var APP_ID = "amzn1.echo-sdk-ams.app.f2a36c58-f9a7-478d-8689-18b0a5ce9b60"; 
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/**
* The AlexaSkill prototype and helper functions
 */
var AlexaSkill = require('./AlexaSkill');
   
var doorControl = function () {
    AlexaSkill.call(this, APP_ID);
};


// Extend AlexaSkill
doorControl.prototype = Object.create(AlexaSkill.prototype);
doorControl.prototype.constructor = doorControl;

//Ignore Certificate errors if using HTTPS communication
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";

doorControl.prototype.intentHandlers = {
        doorIntent: function (intent, session, response) {
        
        //No matter what she wants to tell you her opinion.
        
        function satisfyAlexa() {
                        response.tell("OK");
                        };
        
        // Obtain User Intent
        switch(intent.slots.Control.value) {
                
                // Same button is used
				case "open":
				case "close": 
				case "shut":
				case "stop":
                      path = '/v1/api_transp/NB10XXXX?user=XXXXXXX&pass=XXXXXX&method=POST&reg00=1';
                break;
           
				default:
                         {
                         response.tell("No, I'm sort of busy.  Could you do it?");
                      }
                break;

				
        } 
		var options = {
                     host: local_ip,
                     path: '' + path // Modify if path is prefixed 
					
					
					 
                    };
          var req = http.request(options, satisfyAlexa);
          req.end();						
        }
}


exports.handler = function (event, context) {
       
        var DoorControl = new doorControl();
        DoorControl.execute(event, context);
        
};
