const _this = this;

            const oModel = this.getModel(),
                  sPath  = this.getView().getBindingContext().getPath();

            let aSelectedItems = oEvent.getParameter(Constants.PARAM.SelectedContexts);

            if (aSelectedItems.length === 0){
                MessageBox.information(this.getText("info.noItemSelected"));
                return;
            }

            aSelectedItems.forEach(function (oContext){
                const sProductAddedMsg = _this.getText("info.productAdded", oContext.getObject().ProductID);

                let iQty = oContext.getObject().SelectedQuantity || 1;

                let oNewItem = {
                    OrderNum: oContext.getObject().OrderNum,
                    ProductID: oContext.getObject().ProductID,
                    Quantity: iQty
                };

                oModel.create(sPath + `/${Constants.ENTITY.OrderItem}`, oNewItem, {
                    success: function(){
                        sap.m.MessageToast.show(sProductAddedMsg);
                    }
                });
            });
