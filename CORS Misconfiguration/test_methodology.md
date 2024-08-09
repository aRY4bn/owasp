request header : -> host : target.com/dashboard/user_info 

	- Origin: target.com
			- response header 
			- ACCESS-CONTROL-ALLOW-ORIGIN: target.com
			- ACCESS-Control-ALLOW-Credentials: true
			
	- Origin: sub.target.com 
			- response header 
			- ACCESS-CONTROL-ALLOW-ORIGIN: sub.target.com
			- ACCESS-Control-ALLOW-Credentials: true
		
	- Origin: test.com 
			- response header 
			- ACCESS-CONTROL-ALLOW-ORIGIN: test.com 
			- ACCESS-Control-ALLOW-Credentials: true
	- Origin: null -> when ? 
			- file in system 
			- iframe , sandbox 
	
	
	
	bypass regex origin check : -> target.com
		- target.com.hacker.com
		- target.comhacker.com 
		- hacker.com/?target.com 
		
		
		
		
		
		
