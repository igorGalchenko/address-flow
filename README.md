# address-flow

```js
checkout = {}
addresses = []
defaultAddressId = ""


State (1) - Show address as text

Show shipping Notes

////////////////////////////////


    if (checkout.shippingAddress === null) {
         if (defaultAddressId !== null) {
            checkout.shippingAddress = defaultAddressId (1)
        } else {  // defaultAddress === null
            if (addressess.length > 0) {
                Show address list           (2)
            } else {
                Show empty address form         (3)
            }
        }
    } else { // shipping addres is present in checkout

        Show address as text anyway!!

        onChangeAddressClick({ // When address is shown as text and you click on Edit Address
            if (addressess.length > 0) {
                Show address list     State (2)
                    switch(action) {
                        case Edit: 
                            Modal -> Update in account -> Save in checkout -> Show addr as text (1)
                        case Check:
                            Save -> Save in checkout -> Show addr as text (1)
                        case New:
                            Show empty address form      : State (3)
                            -> Fill Form -> Save in account -> Save in checkout -> Show addr as text (1)
                    }
            } else {/* Hide address list */ }

            ///////////////////////////////////////////

            id = Checkout.shippingAddress.ID = "123" // Id can be null

            if (id == undefined || !(id in address)) { // Empty id or not such id in address list 
                Go to state (3)
                Preset Show empty address form
            } else { // ID in address list
                Make Checked one of radios in the list (2)// Address form is hidden 
            }


        });
    }


    function idIsInAddressList(id, list) { 
        return list.indexOf(id) !== -1;
    }
    
    ```
