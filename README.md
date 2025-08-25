_onBtnPressProductDelete: function(){
            let oTable         = this.byId(Constants.CONTROLS.ProductsTable),
                aSelectedItems = oTable.getSelectedItems();

            if (aSelectedItems.length === 0){
                MessageBox.error(this.getText("error.noSelection"));
                return;
            }

            const sConfirmMsg       = this.getText("confirm.deleteItems", [aSelectedItems.length]),
                  sSuccessDeleteMsg = this.getText("info.successDelete"),
                  sfailedDeleteMsg  = this.getText("error.failedDelete");

            MessageBox.confirm(sConfirmMsg, {
                actions: [MessageBox.Action.YES, MessageBox.Action.NO],
                onClose: function (sAction){
                    if (sAction === MessageBox.Action.YES){
                        let oModel = this.getModel();

                        aSelectedItems.forEach(function (oItem){
                            let sPath = oItem.getBindingContext().getPath();

                            oModel.remove(sPath, {
                                success: function(){
                                    sap.m.MessageToast.show(sSuccessDeleteMsg);
                                    oModel.refresh(true);
                                },
                                error: function(){
                                    MessageBox.error(sfailedDeleteMsg);
                                }
                            });
                        });
                    }
                }.bind(this)
            });
        },
