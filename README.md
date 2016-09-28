# Angular-Development
Applications written in AngularJS

This is a AngularJS Application that uses a public google API to retrieve stock quotes.
The file can be saved to a local file system (name this file with a .HTML extension) and viewed in 
any browser.  Just open the file with a browser from the location that it was saved to.
Seems to work best in Chrome and Firefox.  User can edit the file to specify which stocks to track.

The screen will refresh with the latest quotes (real time) every so many seconds - the interval is
specified as a parameter in the file (paramater name:  pollingInterval).  The default is 5 seconds.

There are several objects inside of the file that must be configured to get the custom display
of stocks/options that the user wants to see on the screen.  Below I list the objects that drive
this applicaton - under configuring the applicaton.

Features of this application:

1) Display of real time stock quotes at an interval that can be customized (default 5 seconds)
2) Display of options - very simple calculation of underlying stock price minus the strike price
   of the option TIMES #shares to give the value of the option.  Note that I do not provide a way
   of intergrating any option premium price into the calculation
3) Dynamic totals are auto calculated as the table reloads with the latest information/prices
4) Ability to turn off (with checkboxes) major averages such as Nasdaq, DOW, or S&P so they do not 
   display in the table.  Also ability to turn off CASH row in table and to hide all Stocks and all
   options.
5) Ability to sort table rows by symbol name by clicking on the "Sybmol" label in the header
6) Ability to filter table by symbol name
7) Ability to see Extended quotes (pre-market or after-market) by selecting the "Extended Trading"
   option in the dropdown
8) Ability to resize the table

Configuring the application

   // need "shares" object for calculation of $Value
   // Note! that the "shares" object must exist even if nothing is in it in witch case it would need to 
	 // be set like this: 	var shares = {};
     var shares = [{"symbol": "MU" , "shares": 1000, "cost": 35}, 
                {"symbol": "AAPL" , "shares": 1000, "cost": 50},
				{"symbol": "GOOG" , "shares": 100, "cost": 550},
				{"symbol": "ORCL" , "shares": 1000, "cost": 35}];
      
     // for tracking options, simple calculation of option price based on price of underlying stock minus strike price
     // no premium is factored in.  
     // Note!!! that if not using options this object still has to exist like: var options = {};
	 var options = [{"t": "Option: MU strike $10, expire: 1/19/2018", "symbol": "MU", "shares": 2000, 
                          "cost": 2.5, "type": "OPT", "strike": 10, "expiration": "1/19/2018"}, 
                 	{"t": "Option: AAPL stk $80, expires on 1/20/2017" , "shares": 1000,  "symbol": "AAPL", 
                          "cost": 54, "type": "OPT", "strike": 80, "expiration": "1/20/2017"}];
        
     // cash on-hand
     // Note!  The cash object must exist exactly as shown below.  If your cash is ZERO then
     // just change the "l" value below to 0 and this way no cash entry will display in the table
     var cash = [{"t": "CASH" , "shares": "1", "l": 1000,  "type": "CASH"}]; 

     // These symbols will be used in the service call to the stock quotation service
     var symbols = [".IXIC", ".DJI", ".INX", "MU", "AAPL", "GOOG", "ORCL"];
	
     // for display of company name associated with ticker
     // AJAX call will populate this object
     var companyName = {};
  
