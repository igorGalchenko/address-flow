# address-flow

```js
checkout = {
     address:    {...}
     ...
}
addresses = [...] // visitor's addresses
visitor.defaultAddressId = "ID" // visitor's default address id

//////////////////////////////////
General Flow
//////////////////////////////////
if (checkout.address === null) {                       // No saved address in checkout
     if (visitor.defaultAddressId !== null) {               // Visitor has default address id
          addr = getAddressById(visitor.defaultAddressId)        // Get default address
          checkoutService.saveAddress(addr)                      // Save it in checkout
          previewAddress()                                       // Show addr as text (1)
     } else {                                               // No default address id
          if (addresses.length > 0) {                            // User has saved addresses
               listAddresses()                                        // Show addr list (2)
          } else {                                               // User doesn't have saved addresses
               showAddressForm()                                      // Show form (3)
          }
    }
} else {                                               // Addres is present in checkout
     previewAddress()                                       // Show addr as text (1)
}

//////////////////////////////////////
function previewAddress()          (1) 
//////////////////////////////////////
     elemAddressBrief(addr)        // Address as text block
     if (isShippingAddress()) {
          elemShippingNotes(addr)  // Shipping notes (for shipping address only)
     }
     elemNextStepAction             // Next step button


     // Actions
     switch(action) {
          case Change:  
               // address ID in checkout
               id = checkout.address.id  
               
               if (id !== null && (id in addresses)) {      // If ID is present in address list
                    listAddresses()                              // Show list (2)
                    selectAddress(id)                            // Select address in list by ID 
                                                                 // TODO: Could be binded ?
               } else {                                     // If ID is null or no such ID in the address list 
                    if (addresses.length > 0) {                  // If User has saved addresses
                         listAddresses()                              // Show list (2)
                    }
                    showAddressForm()                            // Show form (3)
                    presetAddressForm()                          //TODO: Could be binded ?
                    hide elemAddNewAddressAction       	     // New address button
               }
     });
     
////////////////////////////////////////////
function listAddresses()                 (2)
////////////////////////////////////////////
     elemAddressList(addresses)    // Address list block
     elemAddNewAddressAction       // New address button

     // Actions for address list
     switch(action) {
          case Edit(id):
               addr = getAddressById(id)                    // Get address by id 
                                                            // TODO: Always reload from server ?
                                                            
               showModal(addr)                              // Show modal and preset form with address 
                                                            // TODO: Could be binded to the modal form?
                                                            
               validate(addr)                               // Validate form (after submit)
                                                            // TODO: Native angular validation $valid ?
               
               visitorService.updateAddress(id, addr)       // Update address in visitor's account 
                                                            // TODO set as default if checked
                                                            
               checkoutService.saveAddress(addr)            // Save address in checkut
               previewAddress()                             // Show addr as text (1)
               
          case Choose:
               addr = getAddressById(id)                    // Get address by id 
                                                            // TODO: Always reload from server ?
                                                            
               checkoutService.saveAddress(addr)            // Save address in chekcout
               previewAddress()                             // Show addr as text (1)
          
          case New:
               addr = {}                                    // Clear address and address form
               showAddressForm()                            // Show address form (3)
               
     }
     
//////////////////////////////////////////
function showAddressForm()             (3)
//////////////////////////////////////////
     elemForm                           // Form
     elemUseAddressAction               // Use this address button

     // Actions
     switch(action) {                        
          case UseAddress:
               validate(addr)                               // Validate address
                                                            // TODO: Native angular validation $valid ?
                                                            
               if (isLoggedIn) {                            // If visitor is logged in
                    visitorService.saveAddress(addr)             // Save address in visitor's account
                                                                 // TODO set as default if checked
               }
               checkoutService.saveAddress(addr)            // Save adddress in chekcout
               previewAddress()                             // Show addr as text (1)
     }
     

```
