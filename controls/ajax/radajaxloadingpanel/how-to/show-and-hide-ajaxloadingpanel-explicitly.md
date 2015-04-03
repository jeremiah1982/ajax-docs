---
title: Show and Hide AjaxLoadingPanel explicitly
page_title: Show and Hide AjaxLoadingPanel explicitly | UI for ASP.NET AJAX Documentation
description: Show and Hide AjaxLoadingPanel explicitly
slug: ajax/radajaxloadingpanel/how-to/show-and-hide-ajaxloadingpanel-explicitly
tags: show,and,hide,ajaxloadingpanel,explicitly
published: True
position: 0
---

# Show and Hide AjaxLoadingPanel explicitly



## 

To display the loading panel over an element, just call the __Show__ method client-side. This allows you to conditionally display loading panel over updated control (Show the panel in [OnRequestStart]({%slug ajax/client-side-programming/events/onrequeststart%}), and hide it in [OnResponseEnd]({%slug ajax/client-side-programming/events/onresponseend%}) calling the __Hide__ client-side method):

````JavaScript
	    <telerik:RadCodeBlock ID="RadCodeBlock1" runat="server">
	        <script type="text/javascript">
	            var currentLoadingPanel = null;
	            var currentUpdatedControl = null;
	            function RequestStart(sender, args) {
	                currentLoadingPanel = $find("<%= RadAjaxLoadingPanel1.ClientID %>");
	
	                if (args.get_eventTarget() == "<%= Button1.UniqueID %>") {
	                    currentUpdatedControl = "<%= Panel1.ClientID %>";
	                }
	                else {
	                    currentUpdatedControl = "<%= Panel2.ClientID %>";
	                }
	                //show the loading panel over the updated control
	                currentLoadingPanel.show(currentUpdatedControl);
	            }
	            function ResponseEnd() {
	                //hide the loading panel and clean up the global variables
	                if (currentLoadingPanel != null)
	                    currentLoadingPanel.hide(currentUpdatedControl);
	                currentUpdatedControl = null;
	                currentLoadingPanel = null;
	            }
	        </script>
	    </telerik:RadCodeBlock>
````



````XML
	    <telerik:RadScriptManager ID="RadScriptManager1" runat="server">
	    </telerik:RadScriptManager>
	    <telerik:RadAjaxManager ID="RadAjaxManager1" runat="server">
	        <AjaxSettings>
	            <telerik:AjaxSetting AjaxControlID="Button1">
	                <UpdatedControls>
	                    <telerik:AjaxUpdatedControl ControlID="Panel1" LoadingPanelID="RadAjaxLoadingPanel1" />
	                    <telerik:AjaxUpdatedControl ControlID="Panel2" LoadingPanelID="RadAjaxLoadingPanel1" />
	                </UpdatedControls>
	            </telerik:AjaxSetting>
	        </AjaxSettings>
	        <ClientEvents OnRequestStart="RequestStart" OnResponseEnd="ResponseEnd" />
	    </telerik:RadAjaxManager>
	    <telerik:RadAjaxLoadingPanel ID="RadAjaxLoadingPanel1" runat="server" Skin="Default">
	    </telerik:RadAjaxLoadingPanel>
	    <asp:Button ID="Button1" runat="server" Text="Postback" OnClick="Button1_Click" />
	    <asp:Panel ID="Panel1" runat="server" Width="200px">
	        Panel 1
	    </asp:Panel>
	    <asp:Panel ID="Panel2" runat="server" Width="200px">
	        Panel 2
	    </asp:Panel>
````



# See Also

 * [Explicit Show/Hide demo](http://demos.telerik.com/aspnet-ajax/ajax/examples/loadingpanel/explicitshowhide/defaultcs.aspx)