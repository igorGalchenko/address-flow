# address-flow

```js
checkout = {...} // checkout object
addresses = [...] // user addresses
defaultAddressId = "<ID>" // user's default address id



if (checkout.shippingAddress === null) { // No shipping address saved in checkout

     if (defaultAddressId !== null) { // User has default address id
          Flow:
               - Get default address by id
               - Save in checkout
               - Show address as text (1)
          
     } else {  // defaultAddress === null
          if (addresses.length > 0) { // User has saved addresses
               Show address list (2)
          } else { // User doesn't have saved addresses
               Show address form (3.3) // Form visible, 'add new address' hidden
          }
    }
    
} else { // shipping addres is present in checkout
     show address as text (1)
}

//////////////////////////////////////
Show address as text        Point (1) 
///////////////////////////////////////
     Show shipping Notes
     Show 'Next Step' Button

     // Actions
     switch(action) {
          case Change:  // Address is shown as text and user clicks on Edit button
               if (addresses.length > 0) { // User has saved addresses
                    show address list (2)
               }
     
               ID = Checkout.shippingAddress.ID = "<ID>" // address ID saved in checkout
     
               if (ID === null || !(ID in addresses)) { // Null ID or no such ID in the address list 
                    Show address form (3.2) // Form is visible, 'add new address' visible
                    Preset Address Form with saved values
               } else { // ID in address list
                    Check one of the radios in the list
                    Show address form (3.1) // Form is hidden, 'add new address' visible
               }
     });
     
////////////////////////////////////////////
Show address list                 Point (2)
////////////////////////////////////////////
     Show address list
     Show point (3.1)

     // Actions for address list
     switch(action) {
          case Edit:
               Flow:
                    - Show modal 
                    - Validate
                    - Update in account 
                    - Save in checkout 
                    - Show addr as text (1)
          case Choose:
               Flow: 
                    - Save in checkout 
                    - Show addr as text (1)
          
          case New:
               show address form (3.2) // Form visible, 'add new address' visible
               
     }
     
//////////////////////////////////////////
Show address form         Point (3)
//////////////////////////////////////////
     Point (3.1) 
          - form is hidden
          - `add new address` button is visible
     Point (3.2)
          - form is visible
          - `add new address` button is visible
     Point (3.3)
          - form is visible
          - `add new address` button is hidden
     
     // Actions for new address form
     switch(action) {
          case UseAddress:
               - Fill Form 
               - Validate
               - Save in account (if logged in) // Optional
               - Save in checkout
               - Show addr as text (1)
     }
     



function isIdInAddressList(id, list) { 
    return list.indexOf(id) !== -1;
}

```
