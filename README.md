```
workspace "Mechanic tablet system" "Part of bassadone's paperless future" {

    model {
        mechanic = person "Mechanic"
        headMechanic = person "Head Mechanic" "Someone who manages mechanics"
        
        enterprise "Tablet system" {
            desktopClient = softwaresystem "BAPS" "Current baps"  "desktop"
            mobileCLient = softwaresystem "Mobile Clients" "The tablets mechanics will use" "mobile"
            api = softwaresystem "API" {
                authentication = container "Authenitcation" "Authenticates users"  
                failAuthentication = container "Fail Authentication" "User is redirected" "" "failauthentication"
                passAuthentication = container "Pass Authentication" "Process continues"
                process = container "Process" "Data is read to and or written from the database" "" "process"
                return = container "Return" "Any return values are returned back to the client to render" "" "return"
                
            }
            database = softwaresystem "Database" "This stores data" "database"
        }

        # Users and devices
        mechanic -> mobileClient "Uses"
        headMechanic -> mobileClient "Uses"
        headMechanic -> desktopClient "Uses
        desktopClient -> mobileClient "Manages"
        
        # API and authentication
        mobileClient -> authentication "Sends requests"
        desktopClient -> authentication "Sends requests"

        # API Processes        
        authentication -> passAuthentication
        authentication -> failAuthentication
        passAuthentication -> process
        database -> process
        process -> return
    }
         
    views {
        systemlandscape "SystemLandscape" {
            include *
        }
    

        
        container api "Containers" {
            include *
        
            autoLayout lr
        }


        styles {
            element "mobile" {
                shape MobileDevicePortrait
                background #000000
                stroke #808080
            }
            
            element "desktop" {
                shape WebBrowser
                background #000000
                stroke #808080
            }
            
            element "database" {
                shape Cylinder
                background #ffff00
                stroke #FFA500
                color #000000
            }
            
            element "failauthentication" {
                shape Circle
                background #ff0000
            }
            
            element "process" {
                color #000000
                shape Hexagon
                background #ff00ff
            }
            
            element "return" {
                color #000000
                shape Circle
                background #00ffff
            }
        }
    
        theme default
        
    }
}
```
