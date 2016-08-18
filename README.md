# address-flow

```js
checkout = {...} // checkout object
addresses = [...] // user addresses
defaultAddressId = "<ID>" // user's default address id



if (checkout.shippingAddress === null) { // No shipping address saved in checkout

     if (defaultAddressId !== null) { // User has default address id
          checkout.shippingAddress = defaultAddressId  
          show address as text (1) 
     } else {  // defaultAddress === null
          if (addressess.length > 0) { // User has saved addresses
          
               ////////////////////////////////////////////
               Show address list                 State (2)
               ////////////////////////////////////////////
          
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
                         //////////////////////////////////////////
                         Show empty address form         State (3)
                         //////////////////////////////////////////
                         Flow: 
                              - Fill Form 
                              - Validate
                              - Save in account (if logged in) // Optional
                              - Save in checkout
                              - Show addr as text (1)
                }
            
        } else { // User doesn't have saved addresses
            Show empty address form (3)
        }
    }
    
} else { // shipping addres is present in checkout

     //////////////////////////////////////
     Show address as text        State (1) 
     ///////////////////////////////////////
          Show shipping Notes
          Next Step Button only here!!!!

          onChangeAddressClick({ // When address is shown as text and user clicks on Edit button
               if (addresses.length > 0) { // User has saved addresses
                    show address list (2)
               }
     
               ID = Checkout.shippingAddress.ID = "<ID>" // address ID saved in checkout
     
               if (ID === null || !(ID in addresses)) { // Null ID or no such ID in the address list 
                    Show address form (3)
                    Preset Address Form with saved values
               } else { // ID in address list
                    Check one of the radios in the list
               }
          });
}


function isIdInAddressList(id, list) { 
    return list.indexOf(id) !== -1;
}

```
