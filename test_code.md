This file exhbits all the traits of

````ruby
  APP_TYPES = [
    RAVE_MODULES,
    SLAAD,
    JANUS,
    RAVE_ARCHITECT_SECURITY,
    RAVE_ARCHITECT_ROLES,
    RAVE_X,
    RAVE_EDC,
    JUNO
  ]

  MATCHERS_TYPES = {
    /gambit|RaveX(?! )/i => RAVE_X,
    /RaveX? EDC$/i => RAVE_EDC,
    /RaveX? Modules$/i => RAVE_MODULES,
    /slaad|Labs/i => SLAAD,
````
It also contain things like the following:

````cpp
#ifndef Babbage_Bridging_Header_h
#define Babbage_Bridging_Header_h

#import <Babbage/MDClientFactory.h>
#import <Babbage/MDDatastore.h>
#import <Babbage/MDDatastoreFactory.h>
// TODO: Add the other public Babbage classes

#endif /* Babbage_Bridging_Header_h */
````

and then there's:

````swift

import UIKit

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?
    var client: MDClient?
    var UIDatastore: MDDatastore?

    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        // Start AppConnect. This must be done as early as possible during the
        // lifetime of the app, so doing it in the AppDelegate is ideal.
        // The passed directory is used to store the database. The key is used
        // to encrypt sensitive information in the database. It must be 32-bytes
        // long and must be the same between runs.
        let dir = NSFileManager.defaultManager().URLsForDirectory(NSSearchPathDirectory.DocumentDirectory, inDomains: NSSearchPathDomainMask.UserDomainMask).last
        let key = "12345678901234567890123456789012".dataUsingEncoding(NSUTF8StringEncoding)
        MDBabbage.startWithDatastoreAtURL(dir, encryptionKey: key)
        
        // The client that will be used to make requests to the backend can be
        // created once and reused as needed throughout the app
        client = MDClientFactory.sharedInstance().clientOfType(MDClientType.Network)
        
        // All UI code must get objects from the same datastore, so it's a good
        // idea to create it once and make it available to the rest of the app
        UIDatastore = MDDatastoreFactory.create()
        
        return true
    }
}
````
and always ruby turesday

````ruby
class CacheWarmer

  # Invade euresource to force it to make a call to a specific url
  # using the same config it uses for regular calls
  def self.visit(url)
    Euresource.eureka_client.transmit(:uri => url, headers: {'Cache-Control' => 'no-cache, max-age=0'})
  end

end
````

