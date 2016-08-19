# address-flow

```js
checkout = {...} // checkout object
addresses = [...] // user saved addresses
defaultAddressId = "<ID>" // user's default address id

//////////////////////////////////
General Flow
//////////////////////////////////
if (checkout.shippingAddress === null) {     // No address saved in checkout
     if (defaultAddressId !== null) {             // User has default address id
          - Get address by id                          // Get default address
          - Save in checkout                           // Save it in checkout
          - Show address as text (1)                   // Show addr as text
     } else {                                     // No default address id
          if (addresses.length > 0) {                  // User has saved addresses
               - Show address list (2)                      // Show addr list
               - Show address form (3.2)                    // Hide form
          } else {                                     // User doesn't have saved addresses
               - Show address form (3.1)                    // Show form
          }
    }
} else {                                     // Addres is present in checkout
     - Show address as text (1)                   // Show addr as text
}

//////////////////////////////////////
Show address as text        Point (1) 
///////////////////////////////////////
     - Show shipping Notes // For Shipping address only
     - Show 'Next Step' Button

     // Actions
     switch(action) {
          // Address is shown as text and user clicks on Edit button
          case Change:  
               ID = checkout.shippingAddress.ID = "<ID>"    // Get address ID in checkout
               
               if (ID !== undefined && (ID in addresses)) { // ID is present in address list
                    - Show address list (2)                      // Show list
                    - Check one of the radios in the list        // Check list item
                    - Show address form (3.2)                    // Hide form
               } else {                                     // Undefined ID or no such ID in the address list 
                    if (addresses.length > 0) {                  // User has saved addresses
                         - Show address list (2)                      // Show list
                    }
                    - Show address form (3.1)                    // Show form
                    - Preset Address Form with saved values      //TODO: Can be already binded ?
               }
     });
     
////////////////////////////////////////////
Show address list                 Point (2)
////////////////////////////////////////////
     - Show address list
     - Show 'add new address' button

     // Actions for address list
     switch(action) {
          case Edit:
               - Show modal 
               - Validate
               - Update in account 
               - Save in checkout 
               - Show addr as text (1)
               
          case Choose:
               - Save in checkout 
               - Show addr as text (1)
          
          case New:
               - Clear address form
               - Show address form (3.1) // Form visible
               
     }
     
//////////////////////////////////////////
Show address form         Point (3)
//////////////////////////////////////////
     Point (3.1) 
          - form is visible
     Point (3.2)
          - form is hidden

     
     // Actions for new address form
     switch(action) {
          case UseAddress:
               - Validate
               if (loggedIn) {
                    - Save in account 
               }
               - Save in checkout
               - Show addr as text (1)
     }
     

```
