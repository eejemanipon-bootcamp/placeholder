_onBtnPressProductDelete: function(){
            let oTable         = this.byId(Constants.CONTROLS.ProductsTable),
                aSelectedItems = oTable.getSelectedItems(),
                oModel         = this.getModel(),
                sPath          = this.getView().getBindingContext().getPath();

            if (aSelectedItems.length === 0){
                MessageBox.error(this.getText("error.noSelection"));
                return;
            }

            const sConfirmMsg = this.getText("confirm.deleteItems", [aSelectedItems.length]);

            MessageBox.confirm(sConfirmMsg, {
                actions: [MessageBox.Action.YES, MessageBox.Action.NO],
                onClose: function (sAction){
                    if (sAction === MessageBox.Action.YES){
                        // Remove selected items from UI only
                        aSelectedItems.forEach(function (oItem){
                            oModel.remove(sPath + `/${Constants.ENTITY.OrderItem}`, oItem);
                        });
                    }
                }.bind(this)
            });
        },
