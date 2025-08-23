# placeholder
Placeholder text


/**
 * Navigates to a specific route defined in manifest.json.
 *
 * @function
 * @param {string} sRouteName - The name of the route to navigate to.
 * @param {object} [oParams] - Optional route parameters (key-value pairs).
 * @example
 * this.navigateTo("Detail", { productId: "123" });
 */
navigateTo: function(sRouteName, oParams) {
  const oRouter = this.getOwnerComponent().getRouter();
  oRouter.navTo(sRouteName, oParams || {});
},

/**
 * Navigates back using browser history.
 * If no previous hash exists, falls back to a default route.
 *
 * @function
 * @param {string} [sFallbackRoute="Home"] - Optional fallback route name if no history is available.
 * @example
 * this.navigateBack(); // goes back or to "Home"
 * this.navigateBack("MainDashboard"); // custom fallback
 */
navigateBack: function(sFallbackRoute) {
  const oHistory = History.getInstance();
  const sPreviousHash = oHistory.getPreviousHash();

  if (sPreviousHash !== undefined) {
    window.history.go(-1);
  } else {
    const oRouter = this.getOwnerComponent().getRouter();
    oRouter.navTo(sFallbackRoute || "Home", {}, true); // true = replace history
  }
},

/**
 * Navigates directly to the main page, replacing browser history.
 *
 * @function
 * @param {string} [sMainRoute="Home"] - Optional route name for the main page.
 * @example
 * this.navigateToMain(); // navigates to "Home"
 * this.navigateToMain("MainDashboard"); // navigates to custom main page
 */
navigateToMain: function(sMainRoute) {
  const oRouter = this.getOwnerComponent().getRouter();
  oRouter.navTo(sMainRoute || "Home", {}, true); // true = replace history
}
