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
     showAddressBrief(addr)        // Address as text block
     showShippingNotes(addr)       // For shipping address only
     showNexStepAction             // Next step button


     // Actions
     switch(action) {
          case Change:  
               id = checkout.address.id  // address ID in checkout
               
               if (id !== null && (id in addresses)) {      // If ID is present in address list
                    listAddresses()                              // Show list (2)
                    selectAddress(id)                            // Select address in list by ID TODO: Could be binded ?
               } else {                                     // If ID is null or no such ID in the address list 
                    if (addresses.length > 0) {                  // If User has saved addresses
                         listAddresses()                              // Show list (2)
                    }
                    showAddressForm()                            // Show form (3)
                    presetAddressForm()                          //TODO: Could be binded ?
               }
     });
     
////////////////////////////////////////////
function listAddresses()                 (2)
////////////////////////////////////////////
     showAddressList(addresses)    // Address list block
     showAddNewAddressAction       // New address button

     // Actions for address list
     switch(action) {
          case Edit(id):
               addr = getAddressById(id)                    // Get address by id
               showModal(addr)                              // Show modal and preset form with address
               validate(addr)                               // Validate form (after submit)
               visitorService.updateAddress(id, addr)       // Update address in visitor's account
               checkoutService.saveAddress(addr)            // Save address in checkut
               previewAddress()                             // Show addr as text (1)
               
          case Choose:
               addr = getAddressById(id)                    // Get address by id
               checkoutService.saveAddress(addr)            // Save address in chekcout
               previewAddress()                             // Show addr as text (1)
          
          case New:
               addr = {}                                    // Clear address and address form
               showAddressForm()                            // Show address form (3)
               
     }
     
//////////////////////////////////////////
function showAddressForm()             (3)
//////////////////////////////////////////
     showForm                           // Form
     showUseAddressAction               // Use this address button

     // Actions
     switch(action) {                        
          case UseAddress:
               validate(addr)                               // Validate address
               if (isLoggedIn) {                            // If visitor is logged in
                    visitorService.saveAddress(addr)             // Save address in visitor's account
               }
               checkoutService.saveAddress(addr)            // Save adddress in chekcout
               previewAddress()                             // Show addr as text (1)
     }
     

```
