Designer :
---------

<%@ Page Title="" Language="C#" MasterPageFile="~/Modules/Common/Site.Master" AutoEventWireup="true"
    CodeBehind="NotesInfo.aspx.cs" Inherits="ISGN.TCL.Web.Modules.DailyProcessing.NotesInfo" %>

<%@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<%@ Register Assembly="ISGN.TCL.Control.CustomGrid" Namespace="ISGN.TCL.Control.CustomGrid"
    TagPrefix="CustomGid" %>
<%@ Register Assembly="ISGN.TCL.Web.UI.Controls" Namespace="ISGN.TCL.Web.UI.Controls"
    TagPrefix="asp1" %>
<asp:Content ID="Content1" ContentPlaceHolderID="HeadContent" runat="server">
    <link href="../../Styles/tab.css" rel="stylesheet" type="text/css" />
    <link type="text/css" href="../../Styles/tclstlyes.css" rel="stylesheet" />
    <link href="../../Styles/jquery-ui.css" rel="stylesheet" type="text/css" />
    <link type="text/css" media="all" href="../../Styles/jsDatePick_ltr.min.css" rel="stylesheet" />

    <script type="text/javascript" src="../../Scripts/jsDatePick.min.1.3.js"></script>

    <script type="text/javascript" src="../../Scripts/includes.js"></script>

    <script type="text/javascript" src="../../Scripts/jquery-ui.js"></script>

    <script type="text/javascript" src="../../Scripts/jquery.dateentry.js"></script>

    <script src="/Scripts/CustomDataGrid.js" type="text/javascript"></script>

    <script src="../../Scripts/NoteInfo.js" type="text/javascript"></script>

    <script type="text/javascript" src="../../Scripts/jquery.constrain.js"></script>

    <script src="../../Scripts/Validation.js" type="text/javascript"></script>

    <link href="../../Styles/FloatingStyle.css" rel="stylesheet" type="text/css" />

    <script type="text/javascript" language="javascript">
        var FincTabEffctDate1 = '<%= txtFincTabEffctDate1.ClientID %>';
        var FincTabEffctDate2 = '<%= txtFincTabEffctDate2.ClientID %>';
        var FincTabEffctDate3 = '<%= txtFincTabEffctDate3.ClientID %>';

        var FincTabLoanCommit1 = '<%= txtFincTabLoanCommit1.ClientID %>';
        var FincTabLoanCommit2 = '<%= txtFincTabLoanCommit2.ClientID %>';
        var FincTabLoanCommit3 = '<%= txtFincTabLoanCommit3.ClientID %>';

        var FincTabprincBal1 = '<%= txtFincTabprincBal1.ClientID %>';
        var FincTabprincBal2 = '<%= txtFincTabprincBal2.ClientID %>';
        var FincTabprincBal3 = '<%= txtFincTabprincBal3.ClientID %>';

        var FincTabLnLvlDpst1 = '<%= txtFincTabLnLvlDpst1.ClientID %>';
        var FincTabLnLvlDpst2 = '<%= txtFincTabLnLvlDpst2.ClientID %>';
        var FincTabLnLvlDpst3 = '<%= txtFincTabLnLvlDpst3.ClientID %>';

        var FincTabLnLvlEscrw1 = '<%= txtFincTabLnLvlEscrw1.ClientID %>';
        var FincTabLnLvlEscrw2 = '<%= txtFincTabLnLvlEscrw2.ClientID %>';
        var FincTabLnLvlEscrw3 = '<%= txtFincTabLnLvlEscrw3.ClientID %>';

        var FincTabOutEqtyCurrnt = '<%= txtFincTabOutEqtyCurrnt.ClientID %>'
        var FincTabOutEqtyAdjstmnt = '<%= txtFincTabOutEqtyAdjstmnt.ClientID %>'
        var FincTabOutEqtyRslt = '<%= txtFincTabOutEqtyRslt.ClientID %>'

        var FincTabTotlCurnt = '<%= txtFincTabTotlCurnt.ClientID %>'
        var FincTabTotlAdjsmnt = '<%= txtFincTabTotlAdjsmnt.ClientID %>'
        var FincTabTotlRslt = '<%= txtFincTabTotlRslt.ClientID %>'
        var ItemID = '<%= hdnItemID.ClientID %>'
        var FincTabConstCurrnt = '<%= txtFincTabConstCurrnt.ClientID %>';
        var FincTabConstAdjsmnt = '<%= txtFincTabConstAdjsmnt.ClientID %>';
        var FincTabConstRslt = '<%= txtFincTabConstRslt.ClientID %>';
        var IPEffDate = '<%= hdnIPEffDate.ClientID %>';
        var EPEffDate = '<%= hdnEPEffDate.ClientID %>';

        function messageParse(text) {
            //var obj = $.parseJSON(text);
            if (text.length > 0) {
                for (var i = 0; i < text.length; i++) {
                    alert(text[i]);
                }
            }
        }

        function Open() {
            window.showModalDialog("ReleaseScheduleMulti.aspx", "popup_window", "dialogWidth:970px;dialogHeight:700px;")
        }
        function OpenSingle() {

            window.showModalDialog("ReleaseScheduleUpdate.aspx", "popup_window", "dialogWidth:970px;dialogHeight:700px;")

        }

        function WOpen(type, value) {

            var BNo;
            var AuditDate;
            var url;
            var sNote = $("#<%= hdnNoteNo.ClientID %>").val();
            var sUnit = $("#<%= hdnUnitNo.ClientID %>").val();

            if (type == 'udf' || type == 'sc' || type == 'li')
                BNo = $("#<%= hdnBorrowerNo.ClientID %>").val();
            if (type == 'bbu') {
                switch (value) {
                    case '1':
                        AuditDate = $("#<%= txtAuditLog2.ClientID %>").val();
                        url = 'BBUnitAuditLog.aspx?Category=' + value + '&AuditDate=' + AuditDate.replace("/", "-");
                        break;
                    case '3':
                        AuditDate = $("#<%= txtAuditLog1.ClientID %>").val();
                        url = 'BBUnitAuditLog.aspx?Category=' + value + '&AuditDate=' + AuditDate.replace("/", "-");
                        break;
                    case '2':
                        url = 'BBUnitAuditLog.aspx?Category=' + value;
                        break;
                    default:
                        url = 'BBUnitAuditLog.aspx?RecId=' + value;
                        break;
                }

            }
            if (type == 'ip') {
                if (!confirm('This note is part of a Line of Credit that has its own Interest Profiles, create unit profiles anyway?')) {
                    return;
                }
            }

            var vRetrunValue;
            switch (type) {
                case 'udf':
                    var value = 'Note';
                    window.showModalDialog('UserDefinedFieldNoteInfo.aspx?NB=' + BNo + '&ModeBorr=' + value + '&time=' + new Date().getTime() + "&N=" + sNote + "&U=" + sUnit, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:770px;dialogHeight:400px;');
                    break;
                case 'ai':
                    window.showModalDialog('ApprisalInformation.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:1000px;dialogHeight:700px;');
                    break;
                case 'sc':
                    window.showModalDialog('SalescontractInfoNoteInfo.aspx?BNo=' + BNo + '&time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:800px;dialogHeight:600px;');
                    break;
                case 'li':
                    var vli = $("#<%= txtPrjctNetRntArea.ClientID %>").val();
                    var shortDesc = $("#<%= txtPrjctShrtLglDesc.ClientID %>").val();
                    window.showModalDialog('TenantSpaceInfoNote.aspx?id=' + vli + '&BNo=' + BNo + '&time=' + new Date().getTime() + "&ShortDesc=" + shortDesc, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:800px;dialogHeight:600px;');
                    break;
                case 'ip':
                    window.showModalDialog('LineCrdtIntrstPrflNoteinfo.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:700px;dialogHeight:500px;');
                    break;
                case 'bbu':
                    window.showModalDialog(url + '&time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:700px;dialogHeight:500px;');
                    $('#<%=btnRedirectUnits.ClientID%>').click();
                    break;
                case 'bbmu':
                    window.showModalDialog('UnitEditor.aspx?time=' + new Date().getTime() + '&Mode=Note', '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:900px;dialogHeight:700px;');
                    break;
                case 'bbmt':
                    window.showModalDialog('NotesBB_terms.aspx?time=' + new Date().getTime() + '&Mode=Note', '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:980px;dialogHeight:500px;');
                    try { $('#<%=btnRedirectTerms.ClientID%>').click(); } catch (e) { }
                    break;
                case 'bbuf':
                    window.showModalDialog('BBUnitFilter.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:700px;dialogHeight:500px;');
                    $('#<%=btnRedirectUnits.ClientID%>').click();
                    break;
                case 'TEEdit':
                    vRetrunValue = window.showModalDialog('NotesBB_terms.aspx?Edit=' + value + '&time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:980px;dialogHeight:700px;');
                    try { $('#<%=btnRedirectTerms.ClientID%>').click(); } catch (e) { }
                    break;
                case 'doc':
                    window.showModalDialog('DocUpdate.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:700px;dialogHeight:500px;');

                    break;

            }
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                return false;
            }
            else {

                //vRetrunValue                    
            }
        }
        //if INOTE amort, indefault else eqTyp, bdgId                 
        function LoadIPEQWindow(noteNo, unitNo, method, source, borrNo, locseq, locmId, inquiry, indefault, budgetID) {
            var vRetrunValue;
            if (source == "INOTE") {
                vRetrunValue = window.showModalDialog("LineCrdtIntrstPrflNoteinfo.aspx?noteNo=" + noteNo + "&unitNo=" + unitNo + "&method=" + method + "&source=" + source + "&borrNo=" + borrNo + "&locseq=" + locseq + "&locmId=" + locmId + "&inquiry=" + inquiry + "&in=" + indefault, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:1000px;dialogHeight:600px;');
            }
            else {
                vRetrunValue = window.showModalDialog("EquityprofileNoteInfo.aspx?noteNo=" + noteNo + "&unitNo=" + unitNo + "&method=" + method + "&source=" + source + "&borrNo=" + borrNo + "&locseq=" + locseq + "&locmId=" + locmId + "&inquiry=" + inquiry + "&eqTyp=" + indefault + "&bdgId=" + budgetID, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:1000px;dialogHeight:600px;');
            }
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                return false;
            }
            else {
                if (source == "INOTE") {
                    $('#<%=btnIPTemp.ClientID%>').click();
                    return false;
                }
                else {
                    $('#<%=btnEPTemp.ClientID%>').click();
                    return false;
                }
            }
        }

        function ReleaseRebind(text) {
            var vRetrunValue = window.showModalDialog("ReleaseScheduleUpdate.aspx?ItemNo=" + text, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:1000px;dialogHeight:600px;');
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                $('#<%=btnReleaseHide.ClientID%>').click();
                return false;
            }
            else {
                $('#<%=btnReleaseHide.ClientID%>').click();
            }
        }

        function WBOpen() {
            var vRetrunValue;
            vRetrunValue = window.showModalDialog('BdgtItems Noteinfo.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:1200px;dialogHeight:600px;');
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                return false;
            }
            else {
                $('#<%=btnEditBudget.ClientID%>').click();

            }
        }

        function WDocOpen() {
            var vRetrunValue;
            vRetrunValue = window.showModalDialog('DocUpdate.aspx?scname=note&time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:850px;dialogHeight:550px;');
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                return false;
            }
            //            else {
            //                $('#<%=btnEditBudget.ClientID%>').click();

            //            }
        }

        function wNotePayOffOpen(value, type, Mode) {
            var vRetrunValue;
            vRetrunValue = window.showModalDialog('RulesEdit.aspx?Type=' + type + '&Mode=' + Mode + '&RuleID=' + value + '&time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:850px;dialogHeight:500px;');
            if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                return false;
            }
            else {
                if (type == '1') {
                    $('#<%=btnNotePayOff.ClientID%>').click();
                }
                else if (type == '2') {
                    $('#<%= btnReleaseRules.ClientID%>').click();
                }
            }
        }

        function IsGroupEmpty() {
            var vGroup = $("#<%= txtGroupDesc.ClientID %>").val();
            if (vGroup.trim() == '') {
                alert('Please enter a description.');
                return false;
            }
            return true;
        }


        function ConfirmCancel() {
            if (confirm('Are you sure you want to Cancel?') == true) {
                return true;
            }
            else {
                return false;
            }
        }

        function ConfirmCheck(e) {
            if (document.getElementById(ItemID).value == "") {
                alert('Please select a record to delete.');
                return false;
            }
            else {
                if (confirm('Are you sure you want to delete this release schedule?') == true) {
                    return true;
                }
                else {
                    return false;
                }
            }
        }

        function DeleteNotePayOff(e) {
            var result = confirm(e);
            if (result == true) {
                $('#<%=btnNPODelete.ClientID%>').click();
            }
            else {
                return false;
            }
        }

        function DeleteNoteReleasePayOff(e) {
            var result = confirm(e);
            if (result == true) {
                $('#<%=btnRelsRulesDelete.ClientID%>').click();
            }
            else {
                return false;
            }
        }

        function ValidateIP() {
            if (document.getElementById(IPEffDate).value == "") {
                alert('Please select a record to delete.');
                return false;
            }
            else {
                if (confirm("This Will Remove the Highlighted Interest Profile") == true) {
                    return true;
                }
                else {
                    return false;
                }
            }
        }

        function ValidateCopyIP() {
            if (document.getElementById(IPEffDate).value == "") {
                alert('Please select a record to copy.');
                return false;
            }
            else {
                return true;
            }
        }

        function ValidateCopyEP() {
            if (document.getElementById(EPEffDate).value == "") {
                alert('Please select a record to copy.');
                return false;
            }
            else {
                return true;
            }
        }

        function ValidateEP() {
            if (document.getElementById(EPEffDate).value == "") {
                alert('Please select a record to delete.');
                return false;
            }
            else {
                if (confirm("This Will Delete the Highlighted Profile as well as all Duplicate Profiles.  This Operation is Not Recommened.") == true) {
                    return true;
                }

                else {
                    return false;
                }
            }
        }

        function LoadHandler() {
            datpick();
            DatePicker();
        }

        function removeSpecialCharacter(value) {
            if (value.length > 0) {
                var RetValue = value.replace('$', '');
                return RetValue = RetValue.replace(/,/g, '');
            }
            else {
                return value;
            }
        }

        function Commmitment() {

            var vLoanCommitment = $("#<%= txtFincTabLoanCommit3.ClientID %>").val();
            vLoanCommitment = removeSpecialCharacter(vLoanCommitment);
            var decimalval = vLoanCommitment.split(".")[1];

            if (decimalval == null) decimalval = ".00"
            else {
                decimalval = "." + decimalval;
                vLoanCommitment = vLoanCommitment.split(".")[0];
            }
            vLoanCommitment = formatInteger(vLoanCommitment, '###,###,###,###');
            if (vLoanCommitment != '')
                vLoanCommitment = '$' + vLoanCommitment + decimalval;
            $("input[id$='txtBudgetCommitment']").val(vLoanCommitment);
        }

        function TotalEstimated() {

            var vLoanCommitment = $("#<%= txtFincTabTotlRslt.ClientID %>").val();
            vLoanCommitment = removeSpecialCharacter(vLoanCommitment);
            var decimalval = vLoanCommitment.split(".")[1];

            if (decimalval == null) decimalval = ".00"
            else {
                decimalval = "." + decimalval;
                vLoanCommitment = vLoanCommitment.split(".")[0];
            }
            vLoanCommitment = formatInteger(vLoanCommitment, '###,###,###,###');
            if (vLoanCommitment != '')
                vLoanCommitment = '$' + vLoanCommitment + decimalval;
            $("input[id$='txtTotalEstimated']").val(vLoanCommitment);
        }
        function clientActiveTabChanged(sender, args) {

            if (sender.get_activeTabIndex() == 4) {
                if (document.getElementById('<%= hdnBudgetTemp.ClientID %>') != null) {
                    document.getElementById('<%= hdnBudgetTemp.ClientID %>').value = "1";
                    $('#<%=btnSelectBudget.ClientID%>').click();
                }
            }
            //if (sender.get_activeTabIndex() == 10) {
            $('#<%=btnHideKeyContects.ClientID%>').click();

            // }
        }

        function formatInteger(integer, pattern) {

            var result = '';
            integerIndex = integer.length - 1;
            patternIndex = pattern.length - 1;

            while ((integerIndex >= 0) && (patternIndex >= 0)) {
                var digit = integer.charAt(integerIndex);
                integerIndex--;

                // Skip non-digits from the source integer (eradicate current formatting).
                if ((digit < '0') || (digit > '9')) continue;

                // Got a digit from the integer, now plug it into the pattern.
                while (patternIndex >= 0) {
                    var patternChar = pattern.charAt(patternIndex);
                    patternIndex--;

                    // Substitute digits for '#' chars, treat other chars literally.
                    if (digit == '.')
                        break;
                    else if (patternChar == '#') {
                        result = digit + result;
                        break;
                    }
                    else {
                        result = patternChar + result;
                    }
                }
            }

            return result;
        }

        function calculateAdjustment(text, TextValue1, textValue3) {

            var textbox1 = removeSpecialCharacter(document.getElementById(TextValue1).value);
            var textbox3 = removeSpecialCharacter(document.getElementById(textValue3).value);
            var textbox2 = removeSpecialCharacter(text.value);
            if (textbox2.length > 0) {
                textbox3 = parseFloat(textbox1) + parseFloat(textbox2);
                textbox3 = parseFloat(textbox3);
            }
            else {
                textbox3 = parseFloat(textbox1);
                textbox2 = parseFloat("0");
            }
            text.value = dollars(parseFloat(textbox2));
            document.getElementById(textValue3).value = dollars(textbox3);
            //            document.getElementById(BudgetCommitment).value = document.getElementById(textValue3).value;
        }

        function dollars(num) {
            var string = parseFloat(num).toFixed(2);
            var parts = string.split('.');
            var cents = parts.pop();
            var dollars = parts.shift();
            if (num != undefined && num != null && num != '') {
                dollars = dollars.replace(/(\d{1,2}?)((\d{3})+)$/, "$1,$2");
                dollars = dollars.replace(/(\d{3})(?=\d)/g, "$1,");
            }
            return '$' + dollars + '.' + cents;
        }

        function calculateResult(text, TextValue1, TextValue2) {

            var textbox1 = removeSpecialCharacter(document.getElementById(TextValue1).value);
            var textbox2 = removeSpecialCharacter(document.getElementById(TextValue2).value);
            var textbox3 = removeSpecialCharacter(text.value);
            textbox2 = parseFloat(textbox3) - parseFloat(textbox1);
            textbox2 = parseFloat(textbox2);
            if (textbox3.length == 0) {
                textbox3 = parseFloat("0");
                textbox2 = parseFloat(textbox3) - parseFloat(textbox1);
                textbox2 = parseFloat(textbox2);
            }
            text.value = dollars(parseFloat(textbox3));
            document.getElementById(TextValue2).value = dollars(textbox2);
            //            document.getElementById(BudgetCommitment).value = textbox3;
        }


        function CheckBudget() {
            var CValue = document.getElementById('<%=ddlBudgets.ClientID %>');
            var OValue = document.getElementById('<%=hdnBudget.ClientID %>').value;
            if (!confirm('This will Remove any Currently Attached Budgets and Add the Current Selection.?')) {
                CValue.value = OValue
                return false;
            }
            else {
                $('#<%=btnSelectBudget.ClientID%>').click();

            };
        }

        function DeleteBudget(e) {

            var result = confirm(e);
            if (result == true) {
                $('#<%=btnDeleteBudget.ClientID%>').click();
            }
            else {
                return false;
            }
        }

        function CheckNoteProjectSave() {
            var ddlAdmin = $('#<%=drpdwnlstAdmin.ClientID %>').val();
            if (ddlAdmin == '') {
                $('#<%=tblMsg.ClientID %>').show();
                $('#<%=ErrorFail.ClientID %>').show();
                $('#<%=ErrorSuccess.ClientID %>').hide();
                $('#<%=lblErrorFail.ClientID %>').text('Please Assign the Administrator associated for this record');
                return false;
            }
            else {
                $('#<%=tblMsg.ClientID %>').hide();
                $('#<%=ErrorFail.ClientID %>').hide();
                $('#<%=lblErrorFail.ClientID %>').text('');
                if (confirm("Are you sure you want to Save?") == true) {
                    return true;
                }
                else {
                    return false;
                }
            }
        }

        $(function textboxformat() {
            $(".constrain-limit").constrain({
                limit: { "p": 1, "\\": 4 }
            });

            $(".constrain-prohibitalpha").constrain({
                prohibit: { regex: "[a-zA-Z]" }
            });

            $(".constrain-prohibitalphachars").constrain({
                prohibit: { chars: "aeioaAEIOU" }
            });

            $(".constrain-allowalpha").constrain({
                allow: { regex: "[a-zA-Z]" }
            });

            $(".constrain-allowalphachars").constrain({
                allow: { chars: "aeioaAEIOU" }
            });

            $(".double").numeric({ format: "0.0" });

            $(".double-keyup").numeric({ format: "0.00", onblur: false });

            $(".integer").numeric();

        });

        function SelectVendor() {
            var Return;
            Return = window.showModalDialog("VendorSearch.aspx", "popup_window", "dialogWidth:670px;dialogHeight:600px;")

            if (Return != null)
                $("#<%=txtPrjctPrimryContrct.ClientID %>").val(Return.VName);
            return false;
        }

        function WVopen() {
            var vRetrunValue;
            if (document.getElementById('<%=ddlBudgets.ClientID %>').selectedIndex == 0) {
                alert('Please Select a Budget Group.');
                document.getElementById('<%=ddlBudgets.ClientID %>').focus();
                return false;

            }
            else {
                vRetrunValue = window.showModalDialog('MultiVendor.aspx?time=' + new Date().getTime(), '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:910px;dialogHeight:370px;');
                if (vRetrunValue == 'undefined' || vRetrunValue == null) {
                    return false;
                }
                else {
                    return true;

                }
            }
        }


        $(document).ready(function() {
            setDivWidth();
        });
        function setDivWidth() {
            var divWidth = (GetWidth() - 20);
            if (document.getElementById("pnlInterestGrid") != null) {
                document.getElementById("pnlInterestGrid").style.width = divWidth + "px";
            }
            if (document.getElementById("pnlEquityGrid") != null) {
                document.getElementById("pnlEquityGrid").style.width = divWidth + "px";
            }
        }
        function GetWidth() {
            var x = 0;
            if (self.innerHeight) {
                x = self.innerWidth;
            }
            else if (document.documentElement && document.documentElement.clientHeight) {
                x = document.documentElement.clientWidth;
            }
            else if (document.body) {
                x = document.body.clientWidth;
            }
            return x;
        }
        function checkTextAreaMaxLength(textBox, e, length) {

            var maxLength = parseInt(length);
            if (!checkSpecialKeys(e)) {
                if (textBox.value.length > maxLength - 1) {
                    if (window.event)//IE
                    {
                        e.returnValue = false;
                        return false;
                    }
                    else//Firefox
                        e.preventDefault();
                }
            }
        }
        function checkSpecialKeys(e) {
            if (e.keyCode != 8 && e.keyCode != 46 && e.keyCode != 35 && e.keyCode != 36 && e.keyCode != 37 && e.keyCode != 38 && e.keyCode != 39 && e.keyCode != 40)
                return false;
            else
                return true;
        }  
    </script>

    <style type="text/css">
        .modalBackground
        {
            position: absolute;
            background: url(tint20.png) 0 0 repeat;
            background: rgba(0,0,0,0.2);
            border-radius: 14px;
            padding: 8px;
        }
        .pnlBackGround
        {
            border-radius: 8px;
            background: #fff;
            padding: 20px;
        }
    </style>
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="Maincontent" runat="server">
    <asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server" ScriptMode="Release">
    </asp:ToolkitScriptManager>
    <asp:UpdatePanel runat="server" ID="upanel">
        <ContentTemplate>
            <table border="0" width="100%" id="tblMsg" runat="server" cellpadding="5" cellspacing="5"
                style="display: none">
                <tr id="ErrorSuccess" runat="server" style="display: none">
                    <td align="left" valign="middle" class="ErrorSuccess">
                        <asp:Label ID="lblErrorSuccess" runat="server"></asp:Label>
                    </td>
                </tr>
                <tr id="ErrorFail" runat="server" style="display: none">
                    <td align="left" valign="middle" class="ErrorFail">
                        <asp:Label ID="lblErrorFail" runat="server"></asp:Label>
                    </td>
                </tr>
            </table>
            <table align="center" width="100%" cellspacing="0" cellpadding="0" border="0" class="allborder">
                <tr>
                    <td align="left" valign="top">
                        <table border="0" cellspacing="0" cellpadding="0" width="100%" class="allborder">
                            <tr>
                                <td align="left" valign="top" class="gridheaderbg">
                                    <table border="0" cellspacing="0" cellpadding="5" align="left" width="100%">
                                        <tr>
                                            <td>
                                                <asp:Label ID="lblBrwName" runat="server" CssClass="blackbfont"></asp:Label>&nbsp;
                                                <asp:ImageButton ID="imgbtnBrwinfo" runat="server" ImageAlign="Middle" ImageUrl="~/Images/Info.gif"
                                                    AlternateText="BrowerInfo" ToolTip="BrwInfo" />
                                            </td>
                                        </tr>
                                        <%--<tr>
                                            <td align="left" valign="middle">
                                                <asp:Panel ID="pnlbrwinformation" runat="server" class="pnlBackGround">
                                                    <div>
                                                        <table width="100%" align="right">
                                                            <tr>
                                                                <td>
                                                                    <asp:ImageButton ID="imgbtnClosepopup" runat="server" AlternateText="Close" ToolTip="Close"
                                                                        ImageUrl="~/Images/ClosePopup.gif" ImageAlign="Right" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </div>
                                                    <div>
                                                        <table border="0" cellspacing="5" cellpadding="0" align="center" width="100%" class="FilterContent">
                                                            <tr>
                                                                <td width="8%" align="left" valign="middle" class="blucolor blackbfont">
                                                                    Name
                                                                </td>
                                                                <td align="left" valign="middle" width="1%">
                                                                    &nbsp;
                                                                </td>
                                                                <td width="20%" align="left" valign="middle">
                                                                    <asp:Label ID="lblBrwName1" runat="server"></asp:Label>
                                                                </td>
                                                                <td width="10%" align="left" valign="middle" class="blucolor blackbfont">
                                                                    Number
                                                                </td>
                                                                <td width="1%" align="left" valign="middle">
                                                                </td>
                                                                <td width="20%" align="left" valign="middle">
                                                                    <asp:Label ID="lblBrwNumber" runat="server"></asp:Label>
                                                                </td>
                                                                <td width="10%" align="left" valign="middle" class="blucolor blackbfont">
                                                                    Legal Desc
                                                                </td>
                                                                <td width="1%" align="left" valign="middle">
                                                                </td>
                                                                <td width="*" align="left" valign="middle">
                                                                    <asp:Label ID="lblLglDesc" runat="server" Text='<%# ProjectShortLglDesc %>'></asp:Label>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                          <asp:Label ID="lblBrwName3" runat="server"></asp:Label>
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    <asp:Label ID="lblBrwName2" runat="server"></asp:Label>
                                                                </td>
                                                                <td align="left" valign="middle" class="blucolor blackbfont">
                                                                    Telephone
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    <asp:Label ID="lblBrwTelNo" runat="server"></asp:Label>
                                                                </td>
                                                                <td align="left" valign="middle" class="blucolor blackbfont">
                                                                    Tax ID
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    <asp:Label ID="lblBrwTaxId" runat="server"></asp:Label>
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </div>
                                                </asp:Panel>
                                            </td>
                                        </tr>--%>
                                    </table>
                                </td>
                            </tr>
                        </table>
                    </td>
                </tr>
                <tr>
                    <td>
                    </td>
                </tr>
                <tr>
                    <td>
                        <table width="100%" class="allborder" cellpadding="0" cellspacing="0" border="0">
                            <tr>
                                <td>
                                    <%-- <asp:UpdatePanel runat="server" ID="upanel">
                                <ContentTemplate>--%>
                                    <table width="100%" cellpadding="0" cellspacing="0" border="0">
                                        <tr>
                                            <td>
                                                <asp:TabContainer ID="TabNoteInfo" runat="server" ActiveTabIndex="4" CssClass="Tab"
                                                    OnClientActiveTabChanged="clientActiveTabChanged">
                                                    <asp:TabPanel ID="tabPnlProject" runat="server">
                                                        <HeaderTemplate>
                                                            Project</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                            <tr>
                                                                                <td width="100%" align="left" valign="top" class="bgcolor6">
                                                                                    <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                                                        <tr>
                                                                                            <td width="52%">
                                                                                                <table width="96%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                                    <asp:Panel ID="pnlPurchAdd" runat="server">
                                                                                                        <tr height="24">
                                                                                                            <td align="left" valign="middle" class="blackbfont bgcolor4 pl10" colspan="3">
                                                                                                                Property Address
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td width="29%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                Street Address
                                                                                                            </td>
                                                                                                            <td width="1%" align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td width="*" align="left" valign="middle">
                                                                                                                <asp1:TCLTextBox Text='<%# ProjectStreetAddress %>' ID="txtPrjctStrtAddrs" runat="server"
                                                                                                                    CssClass="txtbox" MaxLength="35" BindingName="ProjectStreetAddress" TextValue=""></asp1:TCLTextBox>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                City
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp1:TCLTextBox Text='<%# ProjectCity %>' ID="txtPrjctCity" runat="server" CssClass="txtbox"
                                                                                                                    MaxLength="25" BindingName="ProjectCity" TextValue=""></asp1:TCLTextBox>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                County
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp1:TCLTextBox Text='<%# ProjectCounty %>' ID="txtPrjctCounty" runat="server" CssClass="txtbox"
                                                                                                                    MaxLength="25" BindingName="ProjectCounty" TextValue=""></asp1:TCLTextBox>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                State
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp1:TCLDropDownList ID="drpdwnlstState" runat="server" CssClass="ddlistbox" DataSource='<%# DictStates %>'
                                                                                                                    DataTextField="Value" DataValueField="Key" SetSelectedValue='<%# StateSelectedValue %>'
                                                                                                                    AppendDataBoundItems="True">
                                                                                                                    <asp:ListItem></asp:ListItem>
                                                                                                                </asp1:TCLDropDownList>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                Zip Code
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp:TextBox Text='<%# ProjectZipCode %>' ID="txtPrjctZipCode" runat="server" CssClass="txtbox"
                                                                                                                    MaxLength="10" BindingName="ProjectZipCode" />
                                                                                                                <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender14" runat="server" TargetControlID="txtPrjctZipCode"
                                                                                                                    FilterType="Custom, Numbers" ValidChars="-" Enabled="True" />
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                Country
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp:DropDownList DataSource='<%# DictCountry %>' ID="drpdwnlstCountry" runat="server"
                                                                                                                    CssClass="ddlistbox" DataTextField="Value" DataValueField="Key" AppendDataBoundItems="True">
                                                                                                                    <asp:ListItem></asp:ListItem>
                                                                                                                </asp:DropDownList>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                    </asp:Panel>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Short Legal Description
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp1:TCLTextBox Text='<%# ProjectShortLglDesc %>' ID="txtPrjctShrtLglDesc" runat="server"
                                                                                                                CssClass="txtbox" MaxLength="45" BindingName="ProjectShortLglDesc" TextValue=""></asp1:TCLTextBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <asp:Panel ID="pnlSubDivision" runat="server">
                                                                                                        <tr>
                                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                Sub Division
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                            </td>
                                                                                                            <td align="left" valign="middle">
                                                                                                                <asp1:TCLTextBox Text='<%# ProjectSubDivision %>' ID="txtPrjctSubDiv" runat="server"
                                                                                                                    CssClass="txtbox" MaxLength="25" BindingName="ProjectSubDivision" TextValue=""></asp1:TCLTextBox>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                    </asp:Panel>
                                                                                                    <tr>
                                                                                                        <td colspan="3" align="left" valign="middle">
                                                                                                            <table width="100%" border="0" class="allborder" align="center" cellpadding="0" cellspacing="8">
                                                                                                                <tr height="24">
                                                                                                                    <td colspan="4" align="left" valign="middle" class="blackbfont bgcolor4 pl10">
                                                                                                                        Purpose Of Loan
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Purpose Of Loan
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td width="40%" align="left" valign="middle">
                                                                                                                        <asp1:TCLTextBox Text='<%# ProjectPurchaseOfLoan %>' ID="txtPrjctPurchLoan" runat="server"
                                                                                                                            CssClass="txtboxbig" MaxLength="60" BindingName="ProjectPurchaseOfLoan" TextValue=""></asp1:TCLTextBox>
                                                                                                                    </td>
                                                                                                                    <td width="34%" align="left" valign="middle">
                                                                                                                        <asp:Button ID="btnPrjctUseDfndfld" runat="server" Text="User-Defined Fields" CssClass="btnstylebig"
                                                                                                                            OnClientClick="return WOpen('udf','');" />
                                                                                                                        <asp:HiddenField ID="hdnBorrowerNo" runat="server" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td colspan="3" align="left" valign="middle">
                                                                                                            <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <table width="100%" border="0" class="allborder" align="center" cellpadding="0" cellspacing="8">
                                                                                                                            <asp:Panel ID="pnlPrimaryContractor" runat="server">
                                                                                                                                <tr height="24">
                                                                                                                                    <td colspan="4" align="left" valign="middle" class="blackbfont bgcolor4 pl10">
                                                                                                                                        Primary Contractor
                                                                                                                                    </td>
                                                                                                                                </tr>
                                                                                                                                <tr>
                                                                                                                                    <td width="5%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                                        Vendor
                                                                                                                                    </td>
                                                                                                                                    <td width="20%" align="left" valign="middle">
                                                                                                                                        <asp:TextBox Text='<%# ProjectPrimaryContract %>' ID="txtPrjctPrimryContrct" runat="server"
                                                                                                                                            CssClass="txtbox" ReadOnly="True"></asp:TextBox>&nbsp;
                                                                                                                                        <asp:ImageButton ID="imgbtnPrjctVendor" runat="server" AlternateText="Vendor" ToolTip="VendorSearch"
                                                                                                                                            ImageAlign="Middle" ImageUrl="~/Images/Vendor.png" OnClientClick="javascript:return SelectVendor()" />
                                                                                                                                    </td>
                                                                                                                                    <td width="1%" align="left" valign="middle">
                                                                                                                                    </td>
                                                                                                                                    <td width="10%" align="left" valign="middle">
                                                                                                                                        <asp:CheckBox ID="chkDualAprvl" runat="server" Text="Dual Approval Required for Draw Requests"
                                                                                                                                            Checked='<%# ProjectChkDualApproval %>' Visible='<%# ProjectChkDualApprovalVisible %>'
                                                                                                                                            Enabled='<%# ProjectChkDualApprovalEnabled %>' />
                                                                                                                                    </td>
                                                                                                                                </tr>
                                                                                                                            </asp:Panel>
                                                                                                                            <tr>
                                                                                                                                <td width="20%" colspan="4" align="left" valign="middle">
                                                                                                                                    <asp:Label ID="lblBorrowingBaseMsg" runat="server" CssClass="lblRight" Text="Most information on the 'Project' Tab is not applicable in Borrowing Base Loans. Fields maintained for optional 'User' input." />
                                                                                                                                </td>
                                                                                                                            </tr>
                                                                                                                        </table>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td width="29%" valign="top">
                                                                                                <table>
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="8" class="allborder"
                                                                                                                width="100%">
                                                                                                                <asp:Panel ID="pnlGps" runat="server">
                                                                                                                    <tr height="24">
                                                                                                                        <td align="left" class="blackbfont bgcolor4" colspan="3" valign="middle">
                                                                                                                            GPS Coordinates
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" width="19%" class="blucolor blackbfont">
                                                                                                                            GPS
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle" width="4%">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle" width="77%">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectGPS %>' ID="txtPrjctGPS" runat="server" CssClass="txtbox"
                                                                                                                                MaxLength="15" BindingName="ProjectGPS" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" width="19%" class="blucolor blackbfont">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle" width="4%">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle" width="77%">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectGPS1 %>' ID="txtPrjctGPS1" runat="server" CssClass="txtbox"
                                                                                                                                MaxLength="15" BindingName="ProjectGPS1" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                </asp:Panel>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Account ID
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp1:TCLTextBox Text='<%# ProjectAccId %>' ID="txtPrjctAccID" runat="server" CssClass="txtbox"
                                                                                                                            MaxLength="5" BindingName="ProjectAccId" TextValue=""></asp1:TCLTextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Administrator
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp1:TCLDropDownList ID="drpdwnlstAdmin" runat="server" CssClass="ddlistbox" DataSource='<%# DictProjectAdmin %>'
                                                                                                                            DataTextField="Value" DataValueField="Key" SetSelectedValue='<%# DictProjectAdminSelectedValue %>'>
                                                                                                                        </asp1:TCLDropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <asp:Panel ID="pnlLotSec" runat="server">
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                            Lot
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectLot %>' ID="txtPrjctLot" runat="server" CssClass="txtbox"
                                                                                                                                MaxLength="5" BindingName="ProjectLot" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                            Block
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectBlock %>' ID="txtPrjctBlock" runat="server" CssClass="txtbox"
                                                                                                                                MaxLength="5" BindingName="ProjectBlock" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                            Section
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectSection %>' ID="txtPrjctSection" runat="server"
                                                                                                                                CssClass="txtbox" MaxLength="5" BindingName="ProjectSection" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                            Phase
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectPhase %>' ID="txtPrjctPhase" runat="server" CssClass="txtbox"
                                                                                                                                MaxLength="5" BindingName="ProjectPhase" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                </asp:Panel>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="8" width="100%" class="allborder">
                                                                                                                <asp:Panel ID="pnlTenantSpace" runat="server">
                                                                                                                    <tr height="24">
                                                                                                                        <td align="left" class="blackbfont bgcolor4" colspan="6" valign="middle">
                                                                                                                            Tenant Space
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr>
                                                                                                                        <td align="left" valign="middle" width="35%" colspan="3" class="blucolor blackbfont">
                                                                                                                            Net Rentable Area (sf)
                                                                                                                        </td>
                                                                                                                        <td align="left" valign="middle" width="3%">
                                                                                                                        </td>
                                                                                                                        <td align="right" valign="middle" width="34%">
                                                                                                                            <asp1:TCLTextBox Text='<%# ProjectNetRentArea %>' ID="txtPrjctNetRntArea" runat="server"
                                                                                                                                CssClass="txtbox integer" BindingName="ProjectNetRentArea" TextValue=""></asp1:TCLTextBox>
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                    <tr height="24">
                                                                                                                        <td align="center" valign="middle" colspan="6">
                                                                                                                            <asp:Button ID="btnPjrctLeasingInfo" runat="server" CssClass="btnstylebig" Text="Leasing Info"
                                                                                                                                OnClientClick="return WOpen('li','');" />
                                                                                                                        </td>
                                                                                                                    </tr>
                                                                                                                </asp:Panel>
                                                                                                            </table>
                                                                                                            <table>
                                                                                                                <tr align="center">
                                                                                                                    <td align="center" valign="middle" width="50%">
                                                                                                                        <asp:Button ID="btnPrjctApprslInfo" runat="server" CssClass="btnstylebig" Text="Appraisal Info"
                                                                                                                            OnClientClick="return WOpen('ai','');" />
                                                                                                                    </td>
                                                                                                                    <td align="center" valign="middle" width="50%">
                                                                                                                        <asp:Button ID="btnprjctSalescntrct" runat="server" CssClass="btnstylebig" Text="Sales Contract"
                                                                                                                            OnClientClick="return WOpen('sc','');" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlGeneral" runat="server">
                                                        <HeaderTemplate>
                                                            General</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                            <tr>
                                                                                <td width="100%" align="left" valign="top">
                                                                                    <table width="100%" border="0" cellspacing="0" cellpadding="0" class="bgcolor6 allgborder">
                                                                                        <tr>
                                                                                            <td width="33%" valign="top">
                                                                                                <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8">
                                                                                                    <tr>
                                                                                                        <td width="29%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Company
                                                                                                        </td>
                                                                                                        <td width="3%" align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td width="68%" align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlCompany" runat="server" CssClass="ddlistbox" AutoPostBack="true"
                                                                                                                OnSelectedIndexChanged="ddlCompany_SelectedIndexChanged">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Branch
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlBranch" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Area
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlArea" runat="server" CssClass="ddlistbox" AutoPostBack="true"
                                                                                                                OnSelectedIndexChanged="ddlArea_SelectedIndexChanged">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Locale
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlLocal" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            M-Class
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlMClass" runat="server" CssClass="ddlistbox" AutoPostBack="true"
                                                                                                                OnSelectedIndexChanged="ddlMClass_SelectedIndexChanged">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            S-Class
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlSClass" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Master LOC
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlMLoc" runat="server" CssClass="ddlistbox" AutoPostBack="true"
                                                                                                                OnSelectedIndexChanged="ddlMLoc_SelectedIndexChanged">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Sub LOC
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:DropDownList ID="ddlSLoc" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td colspan="3" align="left" valign="middle">
                                                                                                            &#160;&#160;
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td width="17%" valign="top">
                                                                                                <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8">
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkRevolving" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Revolving
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkNonAccural" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Non Accrual
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkInDefault" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            In Default
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkStopFin" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Stop Financial Activity
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td width="10%" align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkForeclosure" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Foreclosure
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkBankruptcy" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Bankruptcy
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chk203K" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Renovation
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkRollToPerm" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Roll-To-Perm
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:CheckBox ID="chkAssetManagementt" runat="server" />
                                                                                                        </td>
                                                                                                        <td colspan="2" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Asset Management
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td width="50%" valign="top">
                                                                                                <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8">
                                                                                                    <tr>
                                                                                                        <td width="21%" align="left" valign="middle" class="pl10 blucolor blackbfont">
                                                                                                            GL Table
                                                                                                        </td>
                                                                                                        <td width="5%" align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td width="75%" align="left" valign="middle" class="pl20">
                                                                                                            <asp:DropDownList ID="ddlGLTable" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="top" class="pl10 blucolor blackbfont">
                                                                                                            Status
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle" class="pl20">
                                                                                                            <asp:DropDownList ID="ddlStatus" runat="server" CssClass="ddlistbox">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td colspan="3" align="left" valign="top">
                                                                                                            <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blackbfont bgcolor4" colspan="3" style="padding: 5px;">
                                                                                                                        Other Coding
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td width="27%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Federal Code
                                                                                                                    </td>
                                                                                                                    <td width="3%" align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td width="70%" align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlFederalCode" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Loan Grade
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlLoanGrade" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont" cssclass="txtbox">
                                                                                                                        Loan Grade Date
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtLoanGrdDate" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Loan Class
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlLoanClass" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Census Tract
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtCensusTest" runat="server" CssClass="txtbox" MaxLength="10"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Loan Type
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlLoanType" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Loan Purpose
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlLoanPurpose" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Collateral Code
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:DropDownList ID="ddlCollateralCode" runat="server" CssClass="ddlistbox">
                                                                                                                        </asp:DropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Commitment
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtCommitment" runat="server" CssClass="txtbox" MaxLength="5"></asp:TextBox>
                                                                                                                        <%--<asp:Button ID="btnTest" runat="server" Text="Test Save" OnClick="btnSaveTest_Click" />--%>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlDates" runat="server">
                                                        <HeaderTemplate>
                                                            Dates</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                            <%--<tr>
                                                                    <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                        Dates
                                                                    </td>
                                                                    <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                        <img src="../../Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                    </td>
                                                                </tr>--%>
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                            <tr>
                                                                                <td width="100%" align="left" valign="middle" class="bgcolor6">
                                                                                    <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                                                        <tr>
                                                                                            <td width="35%" valign="top">
                                                                                                <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                                    <tr height="24">
                                                                                                        <td colspan="3" align="left" valign="middle" class="bgcolor4 blackbfont tp">
                                                                                                            Pipeline
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td width="34%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Application
                                                                                                        </td>
                                                                                                        <td width="6%" align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td width="60%" align="left" valign="middle">
                                                                                                            <asp:TextBox ID="txtDateTabApplc" runat="server" Text="<%# application %>" CssClass="txtbox"></asp:TextBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Approval
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:TextBox ID="txtDateTabApprvl" runat="server" Text="<%# Approval %>" CssClass="txtbox"></asp:TextBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Closing
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:TextBox ID="txtDateTabClsng" runat="server" Text="<%# Closing %>" CssClass="txtbox"></asp:TextBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                            Percent To Fund
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                        </td>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <asp:TextBox ID="txtDateTabPrcntFund" runat="server" Text="<%# PercenttoFund %>"
                                                                                                                CssClass="txtbox double-keyup" onblur="formatpercentage(this);" onkeypress="return CheckPercentage(this,event);"
                                                                                                                onkeyup="return CheckPercentage(this,event);" onfocus="unformatpercentage(this);"
                                                                                                                onPaste="return false">0.00</asp:TextBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td width="2%">
                                                                                            </td>
                                                                                            <td width="36%">
                                                                                                <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                                                <tr>
                                                                                                                    <td colspan="3" align="left" valign="middle" class="bgcolor4 blackbfont tp">
                                                                                                                        Construction Estimates
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td width="24%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Start
                                                                                                                    </td>
                                                                                                                    <td width="1%" align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td width="*" align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtDateTabCnsStart" runat="server" Text="<%# Start %>" CssClass="txtbox"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Completion
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtDateTabCnsCmpl" runat="server" Text="<%# Completion %>" CssClass="txtbox"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                                                <tr>
                                                                                                                    <td colspan="3" align="left" valign="middle" class="blackbfont bgcolor4 tp">
                                                                                                                        Payoff
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td width="24%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Quoted
                                                                                                                    </td>
                                                                                                                    <td width="1%" align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtDateTabQotPayOff" Text="<%# Quoted %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                                        Posted
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle">
                                                                                                                        <asp:TextBox ID="txtDateTabQotPost" Text="<%# Posted %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td width="29%" valign="top">
                                                                                    <table width="100%" border="0" align="center" cellpadding="0" cellspacing="8" class="allborder">
                                                                                        <tr>
                                                                                            <td colspan="6" align="left" valign="middle" class="bgcolor4 blackbfont tp">
                                                                                                Processing
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td width="19%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                                Note Date
                                                                                            </td>
                                                                                            <td width="1%" align="left" valign="middle">
                                                                                            </td>
                                                                                            <td width="*" align="left" valign="middle">
                                                                                                <asp:TextBox ID="txtDateTabPrssNote" Text="<%# NoteDate %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            </td>
                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                Conversion
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                                <asp:TextBox ID="txtDateTabconvrs" Text="<%# Conversion %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                Maturity
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                                <asp:TextBox ID="txtDateTabMturty" Text="<%# Maturity %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            </td>
                                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                                Rate Lock
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                            </td>
                                                                                            <td align="left" valign="middle">
                                                                                                <asp:TextBox ID="txtDateTabRateLck" Text="<%# RateLock %>" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlRelease" runat="server">
                                                        <HeaderTemplate>
                                                            Release</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td>
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td>
                                                                        <asp:TabContainer ID="tabContainerRelease" runat="server" ActiveTabIndex="1" CssClass="Tab">
                                                                            <asp:TabPanel ID="tabpnlRlsSch" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Release Schedules
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="left" border="0" cellpadding="0" cellspacing="0" width="100%">
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="left" class="bgcolor6 greybborder" valign="top" width="35%">
                                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                                <tr>
                                                                                                                    <td align="left" class="blucolor " valign="middle" width="80%">
                                                                                                                        Number of Additional Release Schedule(s) to Add
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle" width="3%">
                                                                                                                    </td>
                                                                                                                    <td align="left" valign="middle" width="39%">
                                                                                                                        <asp1:TCLNumericTextBox ID="txtRlsSchTabNum" runat="server" BindingName="ReleaseSchNo"
                                                                                                                            CssClass="txtbox" MaxLength="5" Text="<%# ReleaseSchNo %>">
                                                                                                                        </asp1:TCLNumericTextBox>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor6 greybborder" valign="top" width="28%">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor6 greybborder" valign="top" width="29%">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="left" class="bgcolor6" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr class="gridheaderbg">
                                                                                                                    <td align="left" class="pl10" valign="middle">
                                                                                                                        <asp:ImageButton ID="imgbtnRelsSchAdd" runat="server" AlternateText="Add" ToolTip="Add"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon02.png"
                                                                                                                            OnClick="imgbtnRelsSchAdd_Click" vspace="0" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:ImageButton ID="imgbtnRelsSchEdit" runat="server" align="middle" ToolTip="Multi Edit"
                                                                                                                            AlternateText="Multi Edit" border="0" class="curpointer" hspace="0" ImageUrl="~/Images/MultiEdit.png"
                                                                                                                            OnClick="imgbtnRelsSchEdit_Click" vspace="0" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:ImageButton ID="imgbtnRelsSchDel" runat="server" align="middle" ToolTip="Delete"
                                                                                                                            AlternateText="Delete" border="0" class="curpointer" hspace="0" ImageUrl="~/Images/gicon04.png"
                                                                                                                            OnClick="imgbtnRelsSchDel_Click" OnClientClick="return ConfirmCheck(this);" vspace="0" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <CustomGid:ExtendGrid ID="grdRlsSch" runat="server" OnGridCheckedChange="grdRlsSch_GridCheckedChange"
                                                                                                                            OnGridRowEditing="grdRlsSch_GridRowEditing" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <asp:HiddenField ID="hdnItemID" runat="server" />
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                            <asp:TabPanel ID="tabpnlNotePayOffRules" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Note Payoff Rules
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="left" border="0" cellpadding="0" cellspacing="0" width="100%">
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="right" class="bgcolor6" valign="top" width="10%">
                                                                                                            <asp:CheckBox ID="chkPayoffShwAll" runat="server" AutoPostBack="true" Checked="true"
                                                                                                                OnCheckedChanged="chkPayoffShwAll_Checked" />
                                                                                                            Show All
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="31%">
                                                                                                            Borrower Rule Templates
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="top" width="18%">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="41%">
                                                                                                            Attached to Note
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="center" class="bgcolor6" colspan="2" valign="top" width="100%">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="0" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="top">
                                                                                                                        <CustomGid:ExtendGrid ID="cgNotePayOffRules" runat="server" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor1" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="5" width="23%">
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <asp:Button ID="btnPayoffMoveRight" runat="server" CssClass="btnstyle" OnClick="btnPayoffMoveRight_Click"
                                                                                                                            Text="&gt;" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" colspan="2" valign="top" width="100%">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="0" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr>
                                                                                                                    <td align="left" class="gridheaderbg allborder" valign="top">
                                                                                                                        <asp:ImageButton ID="imgbtnNtPayoffRulsDelte" runat="server" AlternateText="Delete"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                            OnClick="imgbtnNtPayoffRulsDelte_Click" ToolTip="Delete" vspace="0" />
                                                                                                                        <asp:ImageButton ID="imgbtnNotePayOffEdit" runat="server" AlternateText="Edit" ImageAlign="Middle"
                                                                                                                            ImageUrl="~/Images/gicon03.png" OnClick="imgbtnNotePayOffEdit_Click" ToolTip="Edit" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:Button ID="btnNPODelete" runat="server" OnClick="btnNPODelete_Click" Style="visibility: hidden" />
                                                                                                                        <asp:Button ID="btnNotePayOff" runat="server" OnClick="btnNotePayOff_Click" Style="visibility: hidden" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <table id="tblNotePayOff" runat="server" border="0" class="bgcolor3 pl10" visible="false"
                                                                                                                            width="100%">
                                                                                                                            <tr>
                                                                                                                                <td align="left" height="5" valign="top">
                                                                                                                                </td>
                                                                                                                            </tr>
                                                                                                                            <tr id="trSuccess" runat="server" visible="false">
                                                                                                                                <td align="left" class="ErrorSuccess" valign="middle">
                                                                                                                                    <asp:Label ID="lblPayOffSuccess" runat="server"></asp:Label>
                                                                                                                                </td>
                                                                                                                            </tr>
                                                                                                                            <tr id="trError" runat="server" visible="false">
                                                                                                                                <td align="left" class="ErrorFail" valign="middle">
                                                                                                                                    <asp:Label ID="lblPayOffError" runat="server" />
                                                                                                                                </td>
                                                                                                                            </tr>
                                                                                                                            <tr>
                                                                                                                                <td align="left" height="5" valign="top">
                                                                                                                                </td>
                                                                                                                            </tr>
                                                                                                                        </table>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="left" valign="top">
                                                                                                                        <CustomGid:ExtendGrid ID="cgNotPayOffRulsAttach" runat="server" GridAllowPaging="True"
                                                                                                                            GridSelectedRowStyleCSS="BlueViolet" GridShowFooter="False" GridWidth="100%"
                                                                                                                            ImageAddButtonEnabled="False" ImageAddButtonToolTip="Add" ImageAddButtonURL="/Images/gicon02.png"
                                                                                                                            ImageAdditionalButton1URL="/Images/gicon02.png" ImageAdditionalButton2URL="/Images/ArrowRightSmall.png"
                                                                                                                            ImageAdditionalButton3URL="/Images/gicon04.png" ImageAdditionalButton4URL="/Images/copy.png"
                                                                                                                            ImageAdditionalButton5URL="/Images/gicon02.png" ImageAdditionalButton6URL="/Images/ArrowRightSmall.png"
                                                                                                                            ImageAdditionalButton7URL="/Images/gicon04.png" ImageAdditionalButton8URL="/Images/copy.png"
                                                                                                                            ImageAddtionalButton1Enabled="False" ImageAddtionalButton2Enabled="False" ImageAddtionalButton3Enabled="False"
                                                                                                                            ImageAddtionalButton4Enabled="False" ImageAddtionalButton5Enabled="False" ImageAddtionalButton6Enabled="False"
                                                                                                                            ImageAddtionalButton7Enabled="False" ImageAddtionalButton8Enabled="False" ImageCopyButtonEnabled="False"
                                                                                                                            ImageCopyButtonToolTip="Copy" ImageCopyButtonURL="/Images/copy.png" ImageDeleteButtonEnabled="False"
                                                                                                                            ImageDeleteButtonToolTip="Delete" ImageDeleteButtonURL="/Images/gicon04.png"
                                                                                                                            ImageEditButtonEnabled="False" ImageEditButtonToolTip="Edit" ImageEditButtonURL="/Images/ArrowRightSmall.png"
                                                                                                                            ImageFirstURL="/Images/LeftAllArrow.png" ImageLastURL="/Images/RightAllArrow.png"
                                                                                                                            ImageNextURL="/Images/RightArrow.png" ImagePreviousURL="/Images/LeftArrow.png"
                                                                                                                            PageNumber="1" SortOrder="ASC" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="right" class="pr10 greyfooter" valign="middle">
                                                                                                <asp:Button ID="btnReleaseHide" runat="server" OnClick="btnReleaseHide_Click" Style="visibility: hidden" />
                                                                                                <asp:HiddenField ID="hdnNotePayOffCount" runat="server" />
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                            <asp:TabPanel ID="tabpnlRules" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Release Rules
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="left" border="0" cellpadding="0" cellspacing="0" width="100%">
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="41%">
                                                                                                            Borrower Rule Templates
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="top" width="18%">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="41%">
                                                                                                            Attached to Release Schedule
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="right" class="bgcolor6" height="30" valign="middle">
                                                                                                            <asp:CheckBox ID="chkRlsRulsShwoAll" runat="server" AutoPostBack="true" Checked="true"
                                                                                                                OnCheckedChanged="chkRlsRulsShwoAll_CheckedChanged" />
                                                                                                            &nbsp; Show All
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="top">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="middle">
                                                                                                            <table border="0" cellpadding="0" cellspacing="8" width="100%">
                                                                                                                <tr>
                                                                                                                    <td class="blucolor blackbfont" width="33%">
                                                                                                                        Release Item
                                                                                                                    </td>
                                                                                                                    <td width="4%">
                                                                                                                        &nbsp;&nbsp;
                                                                                                                    </td>
                                                                                                                    <td width="63%">
                                                                                                                        <asp1:TCLDropDownList ID="drpdwnlstRlsItem" runat="server" AppendDataBoundItems="true"
                                                                                                                            AutoPostBack="true" CssClass="ddlistbox" DataSource="<%# DictReleaseItems %>"
                                                                                                                            DataTextField="Value" DataValueField="Key" OnSelectedIndexChanged="drpdwnlstRlsItem_SelectedIndexChanged"
                                                                                                                            SetSelectedValue="<%# ReleaseItemSelectedValue %>">
                                                                                                                        </asp1:TCLDropDownList>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="center" class="bgcolor6" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <CustomGid:ExtendGrid ID="cstGrdRlsPayoffTemp" runat="server" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="5" width="23%">
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <asp:Button ID="btnRlsRulesMoveRight" runat="server" CssClass="btnstyle" OnClick="btnRlsRulesMoveRight_Click"
                                                                                                                            Text="&gt;" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr>
                                                                                                                    <td align="left" class="gridheaderbg" valign="middle">
                                                                                                                        <asp:ImageButton ID="imgbtnReleaseRule" runat="server" AlternateText="Edit" ImageAlign="Middle"
                                                                                                                            ImageUrl="~/Images/gicon03.png" OnClick="imgbtnReleaseRule_Click" ToolTip="Edit" />
                                                                                                                        &nbsp; &nbsp;<asp:ImageButton ID="imgbtnRelsRulesDel" runat="server" AlternateText="Delete"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                            OnClick="imgbtnRelsRulesDel_Click" ToolTip="Delete" vspace="0" />
                                                                                                                        <asp:Button ID="btnRelsRulesDelete" runat="server" OnClick="btnRelsRulesDelete_Click"
                                                                                                                            Style="visibility: hidden" />
                                                                                                                        <asp:Button ID="btnReleaseRules" runat="server" OnClick="btnReleaseRules_Click" Style="visibility: hidden" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td align="center" cellpadding="0" cellspacing="0" width="100%">
                                                                                                                        <CustomGid:ExtendGrid ID="cstGrdRlsPayoffAtchmnt" runat="server" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="right" class="pr10 greyfooter" colspan="6" valign="middle">
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                        </asp:TabContainer>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlBdgCntrl" runat="server">
                                                        <HeaderTemplate>
                                                            Budget Control</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor6 greybborder"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle" width="8%">
                                                                                            Budgets:
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="1%">
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="32%">
                                                                                            <asp:DropDownList ID="ddlBudgets" runat="server" CssClass="ddlistbox" onchange="return CheckBudget();"
                                                                                                Width="400">
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="59%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Budget Title:
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                        </td>
                                                                                        <td align="left" class="blackbfont" valign="middle">
                                                                                            <asp:Label ID="lblBudgetTitle" runat="server"></asp:Label>
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="gridheaderbg" valign="middle">
                                                                                            <span class="pl10">
                                                                                                <asp:ImageButton ID="imgbtnBdgtCntrlAdd" runat="server" AlternateText="Add" border="0"
                                                                                                    CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon02.png"
                                                                                                    ToolTip="Add" vspace="0" OnClick="imgbtnBdgtCntrlAdd_Click" />
                                                                                                &nbsp;
                                                                                                <asp:ImageButton ID="imgbtnEdit" runat="server" AlternateText="Edit" ImageAlign="Middle"
                                                                                                    ImageUrl="~/Images/gicon03.png" ToolTip="Edit" OnClick="imgbtnEdit_Click" />&nbsp;
                                                                                                <asp:ImageButton ID="imgbtnBdgtCntrlView" runat="server" AlternateText="View" border="0"
                                                                                                    CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon01.png"
                                                                                                    ToolTip="View" vspace="0" Visible="false" />
                                                                                                &nbsp;
                                                                                                <asp:ImageButton ID="ImgbtnDelete" runat="server" AlternateText="Delete" border="0"
                                                                                                    CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                    ToolTip="Delete" vspace="0" OnClick="ImgbtnDelete_Click" />
                                                                                                &nbsp;
                                                                                                <asp:ImageButton ID="imgbtnBdgtCntrlVendor" runat="server" AlternateText="Vendor"
                                                                                                    border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/Vendor.png"
                                                                                                    ToolTip="Vendor" vspace="0" OnClientClick="return WVopen();" />
                                                                                            </span>
                                                                                            <asp:Button runat="server" ID="btnDeleteBudget" Style="visibility: hidden" OnClick="btnDeleteBudget_Click" />
                                                                                            <asp:Button runat="server" ID="btnSelectBudget" Style="visibility: hidden" OnClick="btnSelectBudget_Click" />
                                                                                            <asp:HiddenField ID="hdnBudgetTemp" runat="server" />
                                                                                            <asp:Button runat="server" ID="btnEditBudget" Style="visibility: hidden" OnClick="btnEditBudget_Click" />
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="gridheaderbg" valign="middle">
                                                                                            <table border="0" width="100%" id="tblMsgMPopup" runat="server" visible="false" class="bgcolor3 pl10">
                                                                                                <tr>
                                                                                                    <td align="left" valign="top" height="5">
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr id="trAlertSuccess" runat="server" visible="false">
                                                                                                    <td align="left" valign="middle" class="ErrorSuccess">
                                                                                                        <asp:Label ID="lblSuccess" runat="server" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr id="ErrorAlert1" runat="server" visible="false">
                                                                                                    <td align="left" valign="middle" class="ErrorFail">
                                                                                                        <asp:Label ID="lblErrorAlert" runat="server"></asp:Label>
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" valign="top" height="5">
                                                                                                    </td>
                                                                                                </tr>
                                                                                            </table>
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td>
                                                                                            <CustomGid:ExtendGrid ID="cgBudget" runat="server" />
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor6"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" valign="middle" class="blucolor blackbfont ">
                                                                                            Inspection Company
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            <asp:DropDownList ID="ddlInspCompany" runat="server" CssClass="ddlistbox">
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="left" colspan="3" valign="middle" class="blucolor blackbfont">
                                                                                            <asp:CheckBox ID="chkOmit" runat="server" />
                                                                                            Omit Extended Borrower & Vendor Information From Inspection Requests
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle" width="15%">
                                                                                            Commitment
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="1%">
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="20%">
                                                                                            <asp:TextBox ID="txtBudgetCommitment" runat="server" CssClass="txtbox amount" Enabled="false"></asp:TextBox>
                                                                                        </td>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle" width="15%">
                                                                                            Allocated Commitment
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="1%">
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="*">
                                                                                            <asp:TextBox ID="txtAlctCommit" runat="server" CssClass="txtbox amount" Enabled="false"></asp:TextBox>
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Total Estimated
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            <asp:TextBox ID="txtTotalEstimated" runat="server" CssClass="txtbox amount" Enabled="false"></asp:TextBox>
                                                                                        </td>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Total Allocated
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            <asp:TextBox ID="txtTotalAllocated" runat="server" CssClass="txtbox amount" Enabled="false"></asp:TextBox>
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" class="blucolor blackbfont" valign="middle">
                                                                                            Disbursement Criteria
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                            Auto Generate Borrower Funds First
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            <asp:DropDownList ID="ddlAutoGenBrwFndFirst" runat="server" CssClass="ddlistbox">
                                                                                                <asp:ListItem Text="" Value=""></asp:ListItem>
                                                                                                <asp:ListItem Text="Deposit" Value="D"></asp:ListItem>
                                                                                                <asp:ListItem Text="Escrow" Value="E"></asp:ListItem>
                                                                                                <asp:ListItem Text="None" Value="N" Selected="True"></asp:ListItem>
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="left" colspan="3" valign="middle" class="blucolor blackbfont">
                                                                                            <asp:CheckBox ID="chkOutside" runat="server" />
                                                                                            Outside Equity Last
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                    </td>
                                                                </tr>
                                                                <asp:HiddenField ID="hdnBudget" runat="server" />
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlFinc" runat="server">
                                                        <HeaderTemplate>
                                                            Financial</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                        </table>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor3"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="blackbfont" colspan="5" valign="middle">
                                                                                            Loan Commitment
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" valign="middle" width="29%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle" width="20%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="18%">
                                                                                            Current
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="16%">
                                                                                            Adjustment
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="17%">
                                                                                            Result
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor greybborder" valign="middle">
                                                                                            Loan Commitment
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLoanCommit1" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLoanCommit1 %>'
                                                                                                Enabled="false" BindingName="FincTabLoanCommit1"></asp1:TCLTextBox>
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLoanCommit2" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLoanCommit2 %>'
                                                                                                Enabled="<%# txtFincTabLoanCommit2Enabled %>" BindingName="FincTabLoanCommit2"
                                                                                                OnBlur="calculateAdjustment(this,FincTabLoanCommit1,FincTabLoanCommit3);Commmitment();" />
                                                                                            <asp:FilteredTextBoxExtender ID="txtGroupId_FilterIndex" runat="server" TargetControlID="txtFincTabLoanCommit2"
                                                                                                FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLoanCommit3" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLoanCommit3 %>'
                                                                                                Enabled="<%# txtFincTabLoanCommit3Enabled %>" OnBlur="calculateResult(this,FincTabLoanCommit1,FincTabLoanCommit2);Commmitment();"
                                                                                                BindingName="FincTabLoanCommit3" />
                                                                                            <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender1" runat="server" TargetControlID="txtFincTabLoanCommit3"
                                                                                                FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Effective Date
                                                                                            <asp1:TCLTextBox ID="txtFincTabEffctDate1" runat="server" CssClass="txtbox" Text='<%# FincTabEffctDate1 %>'
                                                                                                BindingName="FincTabEffctDate1" />
                                                                                        </td>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Trancode
                                                                                            <asp:DropDownList ID="drpdwnlstTranscode" runat="server" CssClass="ddlistbox" DataSource='<%# DictTransCode1 %>'
                                                                                                DataTextField="Key" DataValueField="Value" AppendDataBoundItems="true">
                                                                                                <asp:ListItem Text="" Value=""></asp:ListItem>
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="greybborder" valign="middle">
                                                                                            Commitment Rule:
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp:Label ID="lblComRule" Visible='<%# lblComRuleVisible %>' Text='<%# lblComRuleText %>'
                                                                                                runat="server"></asp:Label>
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp:DropDownList ID="drpdwnlstComRule" runat="server" Visible='<%# drpdwnlstComRuleVisible %>'
                                                                                                Enabled='<%# drpdwnlstComRuleEnabled %>' CssClass="ddlistbox" DataSource='<%# DictComRules %>'
                                                                                                DataTextField="Key" DataValueField="value">
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp:Label ID="lblComRulePart0" Text='<%# lblComRulePart0 %>' Visible="false" Width="0px"
                                                                                                runat="server"></asp:Label>
                                                                                            <asp:Label ID="lblComRulePart1" Text='<%# lblComRulePart1 %>' Visible="false" Width="0px"
                                                                                                runat="server"></asp:Label>
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp:Label ID="lblComRulePart2" Text='<%# lblComRulePart2 %>' Visible="false" Width="0px"
                                                                                                runat="server"></asp:Label>
                                                                                            <asp:Label ID="lblComRulePart3" Text='<%# lblComRulePart3 %>' Visible="false" Width="0px"
                                                                                                runat="server"></asp:Label>
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="greybborder" valign="middle">
                                                                                            <asp1:TCLCheckBox ID="chkORComRule" runat="server" Text="Override Rule:" Checked='<%# chkORComRuleChecked %>'
                                                                                                Enabled='<%# chkORComRuleEnabled %>' Visible='<%# chkORComRuleVisible %>' OnCheckedChanged="chkORComRule_Changed" />
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp:Label ID="lblComRuleLong" Visible='<%# lblComRuleLongVisible %>' runat="server"
                                                                                                Text='<%# lblComRuleLongText %>'></asp:Label>
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                    <asp:Panel ID="pnlPricipal" runat="server">
                                                                                        <tr>
                                                                                            <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                                Principal Bal.Cap
                                                                                            </td>
                                                                                            <td align="center" valign="middle">
                                                                                                &nbsp;&nbsp;
                                                                                            </td>
                                                                                            <td align="center" valign="middle">
                                                                                                <asp1:TCLTextBox ID="txtFincTabprincBal1" runat="server" CssClass="txtboxAmt" Text='<%# FincTabprincBal1 %>'
                                                                                                    Enabled="false" BindingName="FincTabprincBal1" />
                                                                                            </td>
                                                                                            <td align="center" valign="middle">
                                                                                                <span class="greybborder">
                                                                                                    <asp1:TCLTextBox ID="txtFincTabprincBal2" runat="server" CssClass="txtboxAmt" Text='<%# FincTabprincBal2 %>'
                                                                                                        BindingName="FincTabprincBal2" onBlur="calculateAdjustment(this,FincTabprincBal1,FincTabprincBal3);" />
                                                                                                    <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender2" runat="server" TargetControlID="txtFincTabprincBal2"
                                                                                                        FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                                </span>
                                                                                            </td>
                                                                                            <td align="center" valign="middle">
                                                                                                <asp1:TCLTextBox ID="txtFincTabprincBal3" runat="server" CssClass="txtboxAmt" Text='<%# FincTabprincBal3 %>'
                                                                                                    OnBlur="calculateResult(this,FincTabprincBal1,FincTabprincBal2);" BindingName="FincTabprincBal3" />
                                                                                                <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender3" runat="server" TargetControlID="txtFincTabprincBal3"
                                                                                                    FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                            </td>
                                                                                        </tr>
                                                                                    </asp:Panel>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor3"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="blackbfont" colspan="5" valign="middle">
                                                                                            Loan Level Deposit
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" valign="middle" width="29%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle" width="20%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="18%">
                                                                                            Current
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="16%">
                                                                                            Adjustment
                                                                                        </td>
                                                                                        <td align="center" class="blucolor greybborder" valign="middle" width="17%">
                                                                                            Result
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor greybborder" valign="middle">
                                                                                            Loan Level Deposit
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLnLvlDpst1" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlDpst1 %>'
                                                                                                Enabled="false" BindingName="FincTabprincBal2" />
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLnLvlDpst2" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlDpst2 %>'
                                                                                                BindingName="FincTabprincBal2" onBlur="calculateAdjustment(this,FincTabLnLvlDpst1,FincTabLnLvlDpst3);" />
                                                                                            <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender4" runat="server" TargetControlID="txtFincTabLnLvlDpst2"
                                                                                                FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                        </td>
                                                                                        <td align="center" class="greybborder" valign="middle">
                                                                                            <asp1:TCLTextBox ID="txtFincTabLnLvlDpst3" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlDpst3 %>'
                                                                                                BindingName="FincTabprincBal2" onBlur="calculateResult(this,FincTabLnLvlDpst1,FincTabLnLvlDpst2);" />
                                                                                            <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender5" runat="server" TargetControlID="txtFincTabLnLvlDpst3"
                                                                                                FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Effective Date
                                                                                            <%--<input id="txtdt18" class="txtbox" type="text" value=" " />--%>
                                                                                            <asp1:TCLTextBox ID="txtFincTabEffctDate2" runat="server" CssClass="txtbox" Text='<%# FincTabEffctDate2 %>'
                                                                                                BindingName="FincTabEffctDate2" />
                                                                                        </td>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                            Trancode
                                                                                            <asp:DropDownList ID="drpdwnlstLnvlDpstEftvTrncode" runat="server" CssClass="ddlistbox"
                                                                                                AppendDataBoundItems="true" DataSource='<%# DictTransCode2 %>' DataTextField="Key"
                                                                                                DataValueField="value">
                                                                                                <asp:ListItem Text="" Value=""></asp:ListItem>
                                                                                            </asp:DropDownList>
                                                                                        </td>
                                                                                        <td align="left" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="center" valign="middle">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="bgcolor6" valign="middle">
                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor3"
                                                                                                width="100%">
                                                                                                <tr>
                                                                                                    <td align="left" class="blackbfont" colspan="5" valign="middle">
                                                                                                        Loan Level Escrow
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" valign="middle" width="29%">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle" width="20%">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="18%">
                                                                                                        Current
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="16%">
                                                                                                        Adjustment
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="17%">
                                                                                                        Result
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" class="blucolor greybborder" valign="middle">
                                                                                                        Loan Level Escrow
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabLnLvlEscrw1" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlEscrw1 %>'
                                                                                                            Enabled="false" BindingName="FincTabLnLvlEscrw1" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabLnLvlEscrw2" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlEscrw2 %>'
                                                                                                            onBlur="calculateAdjustment(this,FincTabLnLvlEscrw1,FincTabLnLvlEscrw3);" BindingName="FincTabLnLvlEscrw2" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender6" runat="server" TargetControlID="txtFincTabLnLvlEscrw2"
                                                                                                            FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabLnLvlEscrw3" runat="server" CssClass="txtboxAmt" Text='<%# FincTabLnLvlEscrw3 %>'
                                                                                                            BindingName="FincTabLnLvlEscrw3" onBlur="calculateResult(this,FincTabLnLvlEscrw1,FincTabLnLvlEscrw2);" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender7" runat="server" TargetControlID="txtFincTabLnLvlEscrw3"
                                                                                                            FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                                        Effective Date
                                                                                                        <%--<input id="txtdt17" class="txtbox" type="text" value=" " />--%>
                                                                                                        <asp1:TCLTextBox ID="txtFincTabEffctDate3" runat="server" CssClass="txtbox" Text='<%# FincTabEffctDate3 %>'
                                                                                                            BindingName="FincTabEffctDate3" />
                                                                                                    </td>
                                                                                                    <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                                        Trancode
                                                                                                        <asp:DropDownList ID="drpdwnlstLnLvlEscrwTrncode" runat="server" CssClass="ddlistbox"
                                                                                                            AppendDataBoundItems="true" DataSource='<%# DictTransCode3 %>' DataTextField="Key"
                                                                                                            DataValueField="Value">
                                                                                                            <asp:ListItem Text="" Value=""></asp:ListItem>
                                                                                                        </asp:DropDownList>
                                                                                                    </td>
                                                                                                    <td align="left" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                </tr>
                                                                                            </table>
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="bgcolor6" valign="top">
                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor3"
                                                                                                width="100%">
                                                                                                <tr>
                                                                                                    <td align="left" class="blackbfont" colspan="5" valign="middle">
                                                                                                        Cost Estimates
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" valign="middle" width="29%">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle" width="20%">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="18%">
                                                                                                        Current
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="16%">
                                                                                                        Adjustment
                                                                                                    </td>
                                                                                                    <td align="center" class="blucolor greybborder" valign="middle" width="17%">
                                                                                                        Result
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" class="blucolor greybborder" valign="middle">
                                                                                                        Outside Equity
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabOutEqtyCurrnt" runat="server" CssClass="txtboxAmt"
                                                                                                            Text='<%# FincTabOutEqtyCurrnt %>' BindingName="FincTabOutEqtyCurrnt" Enabled="false" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabOutEqtyAdjstmnt" runat="server" CssClass="txtboxAmt"
                                                                                                            onBlur="calculateAdjustment(this,FincTabOutEqtyCurrnt,FincTabOutEqtyRslt);" Text='<%# FincTabOutEqtyAdjstmnt %>'
                                                                                                            BindingName="FincTabOutEqtyAdjstmnt" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender8" runat="server" TargetControlID="txtFincTabOutEqtyAdjstmnt"
                                                                                                            FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabOutEqtyRslt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabOutEqtyRslt %>'
                                                                                                            BindingName="FincTabOutEqtyRslt" onBlur="calculateResult(this,FincTabOutEqtyCurrnt,FincTabOutEqtyAdjstmnt);" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender9" runat="server" TargetControlID="txtFincTabOutEqtyRslt"
                                                                                                            FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" class="blucolor greybborder" valign="middle">
                                                                                                        Total
                                                                                                    </td>
                                                                                                    <td align="left" class="greybborder" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabTotlCurnt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabTotlCurnt %>'
                                                                                                            BindingName="FincTabTotlCurnt" Enabled="false" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabTotlAdjsmnt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabTotlAdjsmnt %>'
                                                                                                            BindingName="FincTabTotlAdjsmnt" onBlur="calculateAdjustment(this,FincTabTotlCurnt,FincTabTotlRslt);TotalEstimated();" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender10" runat="server" TargetControlID="txtFincTabTotlAdjsmnt"
                                                                                                            FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                                        </span>
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabTotlRslt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabTotlRslt %>'
                                                                                                            BindingName="FincTabTotlRslt" onBlur="calculateResult(this,FincTabTotlCurnt,FincTabTotlAdjsmnt);TotalEstimated();" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender11" runat="server" TargetControlID="txtFincTabTotlRslt"
                                                                                                            FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td align="left" class="blucolor greybborder" valign="middle">
                                                                                                        Construction
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        &nbsp;&nbsp;
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabConstCurrnt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabConstCurrnt %>'
                                                                                                            Enabled="false" BindingName="FincTabConstCurrnt" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabConstAdjsmnt" runat="server" CssClass="txtboxAmt"
                                                                                                            Text='<%# FincTabConstAdjsmnt %>' BindingName="FincTabConstAdjsmnt" onBlur="calculateAdjustment(this,FincTabConstCurrnt,FincTabConstRslt);" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender12" runat="server" TargetControlID="txtFincTabConstAdjsmnt"
                                                                                                            FilterType="Numbers, Custom" ValidChars="-,.$" Enabled="True" />
                                                                                                    </td>
                                                                                                    <td align="center" class="greybborder" valign="middle">
                                                                                                        <asp1:TCLTextBox ID="txtFincTabConstRslt" runat="server" CssClass="txtboxAmt" Text='<%# FincTabConstRslt %>'
                                                                                                            BindingName="FincTabConstRslt" onBlur="calculateResult(this,FincTabConstCurrnt,FincTabConstAdjsmnt);" />
                                                                                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender13" runat="server" TargetControlID="txtFincTabConstRslt"
                                                                                                            FilterType="Numbers, Custom" ValidChars=",.$" Enabled="True" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                            </table>
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="right" class="pr10 greyfooter" valign="middle">
                                                                                <asp:Button ID="btnFincTabPostFee" runat="server" CssClass="btnstyle" Text="Post Fees"
                                                                                    OnClick="btnFincTabPostFee_Click" />
                                                                                &nbsp;
                                                                            </td>
                                                                        </tr>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlProfiles" runat="server">
                                                        <HeaderTemplate>
                                                            Profiles</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td>
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td>
                                                                        <asp:TabContainer ID="tabcontainterProfiles" runat="server" ActiveTabIndex="0" CssClass="Tab">
                                                                            <asp:TabPanel ID="tabpnlInterestPrfl" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Interest Profiles
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="left" class="bgcolor6" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr class="gridheaderbg">
                                                                                                                    <td align="left" class="pl10" valign="middle">
                                                                                                                        <asp:ImageButton ID="imgbtnIntrstPrflsAdd" runat="server" AlternateText="Add" border="0"
                                                                                                                            CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon02.png"
                                                                                                                            OnClick="ImgbtnIntrstPrflsAdd_Click" ToolTip="Add" vspace="0" />
                                                                                                                        &nbsp;<asp:ImageButton ID="imgbtnIntrstPrflsDel" runat="server" AlternateText="Delete"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                            OnClick="IPImgbtnDelete_Click" ToolTip="Delete" vspace="0" OnClientClick="ValidateIP();" />
                                                                                                                        &nbsp;<asp:ImageButton ID="imgbtnIntrstPrflsCopy" runat="server" AlternateText="Copy"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/copy.png"
                                                                                                                            OnClick="ImgbtnIntrstPrflsCopy_Click" OnClientClick="return ValidateCopyIP();"
                                                                                                                            ToolTip="Copy" vspace="0" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <div id="pnlInterestGrid" class="divscrollcss" style="overflow-x: scroll; height: 200px;">
                                                                                                                            <CustomGid:ExtendGrid ID="CGIntrestProfile" runat="server" OnGridCheckedChange="CGIntrestProfile_GridCheckedChange"
                                                                                                                                OnGridRowEditing="CGIntrestProfile_GridRowEditing" GridAllowPaging="True" GridRowIndex="0"
                                                                                                                                GridSelectedRowStyleCSS="BlueViolet" GridShowFooter="False" GridWidth="100%"
                                                                                                                                ImageAddButtonEnabled="False" ImageAddButtonToolTip="Add" ImageAddButtonURL="/Images/gicon02.png"
                                                                                                                                ImageAdditionalButton1URL="/Images/gicon02.png" ImageAdditionalButton2URL="/Images/ArrowRightSmall.png"
                                                                                                                                ImageAdditionalButton3URL="/Images/gicon04.png" ImageAdditionalButton4URL="/Images/copy.png"
                                                                                                                                ImageAdditionalButton5URL="/Images/gicon02.png" ImageAdditionalButton6URL="/Images/ArrowRightSmall.png"
                                                                                                                                ImageAdditionalButton7URL="/Images/gicon04.png" ImageAdditionalButton8URL="/Images/copy.png"
                                                                                                                                ImageAddtionalButton1Enabled="False" ImageAddtionalButton2Enabled="False" ImageAddtionalButton3Enabled="False"
                                                                                                                                ImageAddtionalButton4Enabled="False" ImageAddtionalButton5Enabled="False" ImageAddtionalButton6Enabled="False"
                                                                                                                                ImageAddtionalButton7Enabled="False" ImageAddtionalButton8Enabled="False" ImageCopyButtonEnabled="False"
                                                                                                                                ImageCopyButtonToolTip="Copy" ImageCopyButtonURL="/Images/copy.png" ImageDeleteButtonEnabled="False"
                                                                                                                                ImageDeleteButtonToolTip="Delete" ImageDeleteButtonURL="/Images/gicon04.png"
                                                                                                                                ImageEditButtonEnabled="False" ImageEditButtonToolTip="Edit" ImageEditButtonURL="/Images/ArrowRightSmall.png"
                                                                                                                                ImageFirstURL="/Images/LeftAllArrow.png" ImageLastURL="/Images/RightAllArrow.png"
                                                                                                                                ImageNextURL="/Images/RightArrow.png" ImagePreviousURL="/Images/LeftArrow.png"
                                                                                                                                PageNumber="1" SortOrder="ASC" />
                                                                                                                        </div>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="right" class="pr10 greyfooter" valign="middle">
                                                                                                            <asp:Button ID="btnTabIntrstprflTranches" runat="server" CssClass="btnstyle" Text="Tranches"
                                                                                                                OnClick="btnTabIntrstprflTranches_Click" />
                                                                                                            <asp:Button ID="btnIPTemp" runat="server" OnClick="btnIPTemp_Click" Style="visibility: hidden" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                            <asp:TabPanel ID="tabPnlEquityPrfl" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Equity Profiles
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="left" class="bgcolor6" valign="top">
                                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                                width="100%">
                                                                                                                <tr class="gridheaderbg">
                                                                                                                    <td align="left" class="pl10" valign="middle">
                                                                                                                        <asp:ImageButton ID="imgbtEqtyPrflsAdd" runat="server" AlternateText="Add" border="0"
                                                                                                                            CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon02.png"
                                                                                                                            OnClick="ImgbtEqtyPrflsAdd_Click" ToolTip="Add" vspace="0" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:ImageButton ID="imgbtEqtyPrflsDel" runat="server" AlternateText="Delete" border="0"
                                                                                                                            CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                            OnClick="imgbtEqtyPrflsDel_Click" OnClientClick="return ValidateEP();" ToolTip="Delete"
                                                                                                                            vspace="0" />
                                                                                                                        &nbsp;<asp:ImageButton ID="imgbtEqtyPrflsCopy" runat="server" AlternateText="Copy"
                                                                                                                            border="0" CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/copy.png"
                                                                                                                            OnClick="imgbtEqtyPrflsCopy_Click" OnClientClick="return ValidateCopyEP();" ToolTip="Copy"
                                                                                                                            vspace="0" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <div id="pnlEquityGrid" class="divscrollcss" style="overflow-x: auto; overflow-y: auto;">
                                                                                                                            <CustomGid:ExtendGrid ID="CGEquityProfile" runat="server" OnGridCheckedChange="CGEquityProfile_GridCheckedChange"
                                                                                                                                OnGridRowEditing="CGEquityProfile_GridRowEditing" />
                                                                                                                        </div>
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="right" class="pr10 greyfooter" valign="middle">
                                                                                                            <asp:Button ID="btnEPTemp" runat="server" OnClick="btnEPTemp_Click" Style="visibility: hidden" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                        </asp:TabContainer>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlAtchmnt" runat="server">
                                                        <HeaderTemplate>
                                                            Documents</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td>
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td>
                                                                        <asp:TabContainer ID="tabcontainerAttachemnts" runat="server" ActiveTabIndex="1"
                                                                            AutoPostBack="True" CssClass="Tab">
                                                                            <asp:TabPanel ID="tabpnlDocTrack" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Doc Tracking
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="left" border="0" cellpadding="0" cellspacing="0" width="100%">
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                                    <tr>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="41%">
                                                                                                            Standard Document Templates
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="top" width="18%">
                                                                                                            &nbsp;&nbsp;
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="top" width="41%">
                                                                                                            Attached to Note
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td align="center" class="bgcolor6" valign="middle">
                                                                                                            <asp:ListBox ID="lstbStndardArtchBrwDocTrack" runat="server" CssClass="textareafont"
                                                                                                                AutoPostBack="true" DataSource="<%# dsDockTracking %>" DataTextField="DESCRIP"
                                                                                                                DataValueField="DESCRIP" OnSelectedIndexChanged="lstbStndardArtchBrwDocTrack_SelectedIndexChanged"
                                                                                                                SelectionMode="Multiple" Style="width: 95%; height: 100px"></asp:ListBox>
                                                                                                        </td>
                                                                                                        <td align="left" class="bgcolor1" valign="middle">
                                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="5" width="23%">
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <asp:Button ID="btnDoctMove" runat="server" CssClass="btnstyle" OnClick="btnDoctMove_Click"
                                                                                                                            Enabled="false" Text="&gt;" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                                <tr>
                                                                                                                    <td>
                                                                                                                        <asp:Button ID="btnDocRemove" runat="server" CssClass="btnstyle" OnClick="btnDocRemove_Click"
                                                                                                                            Enabled="false" Text="&lt;" />
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                        <td align="center" class="bgcolor6" valign="middle">
                                                                                                            <asp:ImageButton ID="imgbtnDocTracAdd" runat="server" AlternateText="Add" ImageAlign="Middle"
                                                                                                                ImageUrl="~/Images/gicon02.png" ToolTip="Add" Visible="false" OnClick="imgbtnDocTracAdd_Click" />
                                                                                                            &nbsp;
                                                                                                            <asp:ImageButton ID="imgbtnDocTracEdit" Visible="false" runat="server" AlternateText="Edit"
                                                                                                                ImageAlign="Middle" ImageUrl="~/Images/gicon03.png" ToolTip="Edit" OnClick="imgbtnDocTracEdit_Click" />
                                                                                                            &nbsp;
                                                                                                            <%--   <asp:ImageButton ID="imgbtnDocTracDel" runat="server" AlternateText="Delete" ToolTip="Delete"
                                                                                                                        ImageAlign="Middle" ImageUrl="~/Images/gicon04.png" />&nbsp;--%>
                                                                                                            <br />
                                                                                                            <asp:ListBox ID="lstbArtchBrwDocTrack" runat="server" CssClass="textareafont" DataSource="<%# dsDockTracking2 %>"
                                                                                                                AutoPostBack="true" DataTextField="DOC" DataValueField="DOC" OnSelectedIndexChanged="lstbArtchBrwDocTrack_SelectedIndexChanged"
                                                                                                                SelectionMode="Multiple" Style="width: 95%; height: 100px"></asp:ListBox>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="right" class="pr10 greyfooter" colspan="6" valign="middle">
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                            <asp:TabPanel ID="tblpnlAttachmets" runat="server">
                                                                                <HeaderTemplate>
                                                                                    Attachments
                                                                                </HeaderTemplate>
                                                                                <ContentTemplate>
                                                                                    <table border="0" cellpadding="1" cellspacing="0" class="allgborder" width="100%">
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="left" border="0" cellpadding="0" cellspacing="0" width="100%">
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top">
                                                                                                <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                    width="100%">
                                                                                                    <tr>
                                                                                                        <td align="left" valign="middle">
                                                                                                            <table align="center" border="0" cellpadding="5" cellspacing="1" class="gridheaderbg"
                                                                                                                width="100%">
                                                                                                                <tr>
                                                                                                                    <td align="left" class="pl10" valign="middle">
                                                                                                                        <asp:ImageButton ID="imgbtnAtchmntsAdd" runat="server" AlternateText="Add" border="0"
                                                                                                                            CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon13.png"
                                                                                                                            OnClick="imgbtnAtchmntsAdd_Click" ToolTip="Attach" vspace="0" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:ImageButton ID="imgbtnAtchmntsDel" runat="server" AlternateText="Delete" border="0"
                                                                                                                            CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                            ToolTip="Delete" vspace="0" Enabled="False" OnClick="imgbtnAtchmntsDel_Click" />
                                                                                                                        &nbsp;
                                                                                                                        <asp:ImageButton ID="imgbtnAttachDetails" runat="server" AlternateText="Details"
                                                                                                                            CssClass="curpointer" ImageAlign="AbsMiddle" ImageUrl="~/Images/application_view_list.png"
                                                                                                                            OnClick="imgbtnAttachDetails_Click" ToolTip="Details" Enabled="False" />
                                                                                                                        &nbsp;
                                                                                                                    </td>
                                                                                                                </tr>
                                                                                                            </table>
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <CustomGid:ExtendGrid ID="gvAttachments" runat="server" GridAllowPaging="True" GridRowIndex="0"
                                                                                                                GridSelectedRowStyleCSS="BlueViolet" GridShowFooter="False" GridWidth="100%"
                                                                                                                ImageAddButtonEnabled="False" ImageAddButtonToolTip="Add" ImageAddButtonURL="/Images/gicon02.png"
                                                                                                                ImageAdditionalButton1URL="/Images/gicon02.png" ImageAdditionalButton2URL="/Images/ArrowRightSmall.png"
                                                                                                                ImageAdditionalButton3URL="/Images/gicon04.png" ImageAdditionalButton4URL="/Images/copy.png"
                                                                                                                ImageAdditionalButton5URL="/Images/gicon02.png" ImageAdditionalButton6URL="/Images/ArrowRightSmall.png"
                                                                                                                ImageAdditionalButton7URL="/Images/gicon04.png" ImageAdditionalButton8URL="/Images/copy.png"
                                                                                                                ImageAddtionalButton1Enabled="False" ImageAddtionalButton2Enabled="False" ImageAddtionalButton3Enabled="False"
                                                                                                                ImageAddtionalButton4Enabled="False" ImageAddtionalButton5Enabled="False" ImageAddtionalButton6Enabled="False"
                                                                                                                ImageAddtionalButton7Enabled="False" ImageAddtionalButton8Enabled="False" ImageCopyButtonEnabled="False"
                                                                                                                ImageCopyButtonToolTip="Copy" ImageCopyButtonURL="/Images/copy.png" ImageDeleteButtonEnabled="False"
                                                                                                                ImageDeleteButtonToolTip="Delete" ImageDeleteButtonURL="/Images/gicon04.png"
                                                                                                                ImageEditButtonEnabled="False" ImageEditButtonToolTip="Edit" ImageEditButtonURL="/Images/ArrowRightSmall.png"
                                                                                                                ImageFirstURL="/Images/LeftAllArrow.png" ImageLastURL="/Images/RightAllArrow.png"
                                                                                                                ImageNextURL="/Images/RightArrow.png" ImagePreviousURL="/Images/LeftArrow.png"
                                                                                                                PageNumber="1" SortOrder="ASC" OnGridCheckedChange="gvAttachments_GridCheckedChange"
                                                                                                                OnGridRowEditing="gvAttachments_GridRowEditing" OnGridRowCreated="gvAttachments_GridRowCreated"
                                                                                                                OnGridPaging="gvAttachments_GridPaging" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="right" class="pr10 greyfooter" valign="middle">
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </ContentTemplate>
                                                                            </asp:TabPanel>
                                                                        </asp:TabContainer>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlBrwBasTerms" runat="server">
                                                        <HeaderTemplate>
                                                            Borrowing Base Terms</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <CustomGid:ExtendGrid ID="CstGrdBrwBaseTerms" GridRowStyleCSS="normalrow" GridHeaderRowCSS="pl10 pr10 gridheader"
                                                                            GridAlternatingRowCSS="altrow" OnGridRowEditing="CstGrdBrwBaseTerms_OnGridRowEditing"
                                                                            runat="server" />
                                                                    </td>
                                                                </tr>
                                                                <tr>
                                                                    <td align="right">
                                                                        <asp:Button ID="btnBrwBaseMngTrms" runat="server" CssClass="btnstylebig" OnClientClick="return WOpen('bbmt','');"
                                                                            Text="Manage Terms" />
                                                                        <asp:Button ID="btnRedirectTerms" runat="server" OnClick="btnRedirectTerms_Click"
                                                                            Style="display: none" />
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlBrwBasUnits" runat="server">
                                                        <HeaderTemplate>
                                                            Borrowing Base Units
                                                        </HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td align="left" valign="top">
                                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                        </table>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td>
                                                                                            <CustomGid:ExtendGrid ID="GVUnitTerms" runat="server" GridWidth="100%" GridHeaderRowCSS="pl10 pr10 gridheader"
                                                                                                GridAlternatingRowCSS="altrow" GridRowStyleCSS="normalrow" />
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td>
                                                                                <table cellpadding="0" cellspacing="0" border="0" width="100%">
                                                                                    <tr>
                                                                                        <td width="25%">
                                                                                            <asp:CheckBox ID="chkPostInspections" runat="server" Text="Post Inspections Using Budget Processing" />
                                                                                        </td>
                                                                                        <td width="20%">
                                                                                            <asp:CheckBox ID="chkStartPipeline" runat="server" Text="New Units start in Pipeline" />
                                                                                        </td>
                                                                                        <td align="right" valign="top">
                                                                                            <asp:Button ID="btnBrwBaseFilter" runat="server" CssClass="btnstylebig" OnClientClick="return WOpen('bbuf',1);"
                                                                                                Text="Filter" />
                                                                                            &nbsp;&nbsp;
                                                                                            <asp:Button ID="btnBrwBaseMangUnits" runat="server" CssClass="btnstylebig" OnClientClick="return WOpen('bbmu','');"
                                                                                                Text="Manage Units" />
                                                                                            <asp:Button ID="btnRedirectUnits" Style="display: none" runat="server" OnClick="btnRedirectUnits_Click">
                                                                                            </asp:Button>
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="top">
                                                                                <table align="center" border="0" cellpadding="5" cellspacing="0" class="bgcolor6"
                                                                                    width="100%">
                                                                                    <tr>
                                                                                        <td align="left" class="bgcolor4 blackbfont" colspan="6" valign="middle">
                                                                                            Audit Log
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle" width="10%">
                                                                                            Reconciled Never
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="1%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="*">
                                                                                            <asp:TextBox ID="txtAuditLog1" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            <%--<asp:TextBox ID="txtAuditLog1" runat="server" CssClass="txtbox"></asp:TextBox>--%>
                                                                                            &nbsp;<asp:Button ID="btnBrwBstabLogUnit1" runat="server" CssClass="btnstyle" OnClientClick="return WOpen('bbu','3');"
                                                                                                Text="Log" />
                                                                                        </td>
                                                                                        <td align="left" class="blucolor blackbfont" valign="middle" width="15%">
                                                                                            Audited Never
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="1%">
                                                                                            &nbsp;&nbsp;
                                                                                        </td>
                                                                                        <td align="left" valign="middle" width="*">
                                                                                            <asp:TextBox ID="txtAuditLog2" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                            &nbsp;&nbsp;<asp:Button ID="btnBrwBstabLogUnit2" runat="server" CssClass="btnstyle"
                                                                                                OnClientClick="return WOpen('bbu','1');" Text="Log" />
                                                                                        </td>
                                                                                    </tr>
                                                                                    <tr>
                                                                                        <td align="left" colspan="6" valign="middle">
                                                                                            <table align="center" border="0" cellpadding="0" cellspacing="1" class="allborder"
                                                                                                width="100%">
                                                                                                <tr>
                                                                                                    <td align="left" class="gridheaderbg" valign="middle">
                                                                                                        <asp:ImageButton ID="ImgAuditAdd" runat="server" ImageAlign="Middle" ImageUrl="~/Images/gicon02.png"
                                                                                                            AlternateText="Add" ToolTip="Add" OnClientClick="return WOpen('bbu','2');" />&nbsp;
                                                                                                        <asp:ImageButton ID="ImgAuditDelete" runat="server" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                            OnClick="ImgAuditDelete_Click" AlternateText="Delete" ToolTip="Delete" />
                                                                                                        <asp:HiddenField ID="hdnAuditDelete" runat="server" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                                <tr>
                                                                                                    <td>
                                                                                                        <CustomGid:ExtendGrid ID="GVUnitAuditLog" runat="server" GridWidth="100%" GridHeaderRowCSS="pl10 pr10 gridheader"
                                                                                                            GridAlternatingRowCSS="altrow" GridRowStyleCSS="normalrow" OnGridCheckedChange="GVUnitAuditLog_GridCheckedChange"
                                                                                                            OnGridRowEditing="GVUnitAuditLog_GridRowEditing" />
                                                                                                    </td>
                                                                                                </tr>
                                                                                            </table>
                                                                                        </td>
                                                                                    </tr>
                                                                                </table>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="right" class="pr10 greyfooter" valign="middle">
                                                                            </td>
                                                                        </tr>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                    <asp:TabPanel ID="tabPnlkyCnt" runat="server">
                                                        <HeaderTemplate>
                                                            Key Contacts</HeaderTemplate>
                                                        <ContentTemplate>
                                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                <tr>
                                                                    <td>
                                                                        <asp:Button runat="server" ID="btnHideKeyContects" Style="visibility: hidden" OnClick="btnHideKeyContects_Click" />
                                                                        <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                                            <tr>
                                                                                <td align="left" valign="top">
                                                                                    <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td align="left" valign="top">
                                                                                    <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                                        <tr>
                                                                                            <td colspan="1" align="center" valign="top" class="blackbfont bgcolor6">
                                                                                                Key Contacts Templates
                                                                                            </td>
                                                                                            <td width="18%" align="left" valign="top" class="bgcolor1">
                                                                                                &#160;&#160;
                                                                                            </td>
                                                                                            <td width="41%" align="center" valign="top" class="blackbfont bgcolor6">
                                                                                                Attached Key Contacts
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="left" valign="top" class="bgcolor6">
                                                                                                <table width="100%" border="0" cellspacing="8" cellpadding="0">
                                                                                                    <tr>
                                                                                                        <td width="34%">
                                                                                                            <asp:DropDownList ID="ddlKeyContacts" runat="server" CssClass="ddlistbox" AutoPostBack="True"
                                                                                                                OnSelectedIndexChanged="ddlKeyContacts_SelectedIndexChanged">
                                                                                                            </asp:DropDownList>
                                                                                                        </td>
                                                                                                        <td width="25%" nowrap="nowrap">
                                                                                                            <span class="bgcolor3" class="blucolor blackbfont">Find Contact </span>
                                                                                                        </td>
                                                                                                        <td width="32%" valign="middle">
                                                                                                            <asp:TextBox ID="txtFindContact" runat="server" Style="height: 12px;"></asp:TextBox>
                                                                                                        </td>
                                                                                                        <td width="5%" valign="middle">
                                                                                                            <asp:ImageButton ID="btnFind" runat="server" OnClick="btnFind_Click" ToolTip="Find"
                                                                                                                ImageUrl="~/Images/gicon01.png" vspace="0" hspace="0" border="0" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td align="left" valign="top" class="bgcolor1">
                                                                                                &#160;&#160;
                                                                                            </td>
                                                                                            <td align="left" valign="top" class="bgcolor6">
                                                                                                &#160;&#160;
                                                                                            </td>
                                                                                        </tr>
                                                                                        <tr>
                                                                                            <td align="center" valign="top" class="bgcolor6">
                                                                                                <table border="0" cellspacing="1" cellpadding="0" width="100%" align="center" class="allborder">
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <CustomGid:ExtendGrid runat="server" ID="csKeyContacts" GridAllowPaging="True" GridSelectedRowStyleCSS="BlueViolet"
                                                                                                                GridShowFooter="False" GridWidth="100%" ImageAddButtonEnabled="False" ImageAddButtonURL="/Images/gicon02.png"
                                                                                                                ImageAdditionalButton1URL="/Images/gicon02.png" ImageAdditionalButton2URL="/Images/ArrowRightSmall.png"
                                                                                                                ImageAdditionalButton3URL="/Images/gicon04.png" ImageAdditionalButton4URL="/Images/copy.png"
                                                                                                                ImageAdditionalButton5URL="/Images/gicon02.png" ImageAdditionalButton6URL="/Images/ArrowRightSmall.png"
                                                                                                                ImageAdditionalButton7URL="/Images/gicon04.png" ImageAdditionalButton8URL="/Images/copy.png"
                                                                                                                ImageAddtionalButton1Enabled="False" ImageAddtionalButton2Enabled="False" ImageAddtionalButton3Enabled="False"
                                                                                                                ImageAddtionalButton4Enabled="False" ImageAddtionalButton5Enabled="False" ImageAddtionalButton6Enabled="False"
                                                                                                                ImageAddtionalButton7Enabled="False" ImageAddtionalButton8Enabled="False" ImageCopyButtonEnabled="False"
                                                                                                                ImageCopyButtonURL="/Images/copy.png" ImageDeleteButtonEnabled="False" ImageDeleteButtonURL="/Images/gicon04.png"
                                                                                                                ImageEditButtonEnabled="False" ImageEditButtonURL="/Images/ArrowRightSmall.png"
                                                                                                                ImageFirstURL="/Images/LeftAllArrow.png" ImageLastURL="/Images/RightAllArrow.png"
                                                                                                                ImageNextURL="/Images/RightArrow.png" ImagePreviousURL="/Images/LeftArrow.png"
                                                                                                                PageNumber="1" ImageAddButtonToolTip="Add" ImageCopyButtonToolTip="Copy" ImageDeleteButtonToolTip="Delete"
                                                                                                                ImageEditButtonToolTip="Edit" SortOrder="ASC" OnGridCheckedChange="csKeyContacts_GridCheckedChange"
                                                                                                                GridRowIndex="0" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <asp:Panel ID="pnlKeyContact" runat="server" Visible="false">
                                                                                                        <tr>
                                                                                                            <td>
                                                                                                                <asp:Label ID="lblRec1" runat="server" Text="No Records to Display!!!"></asp:Label>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                    </asp:Panel>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td align="left" valign="top" class="bgcolor1">
                                                                                                <table width="23%" border="0" align="center" cellpadding="5" cellspacing="5">
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <asp:Button ID="btnKeyCntsMoveRight" runat="server" CssClass="btnstyle" Text="&gt;"
                                                                                                                OnClick="btnKeyCntsMoveRight_Click" Enabled="False" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                </table>
                                                                                            </td>
                                                                                            <td align="center" valign="top" class="bgcolor6">
                                                                                                <table border="0" cellspacing="1" cellpadding="0" width="100%" align="center" class="allborder">
                                                                                                    <tr>
                                                                                                        <td align="left" class="gridheaderbg" valign="top">
                                                                                                            <asp:ImageButton ID="imgbtnDKeyContact" runat="server" AlternateText="Delete" border="0"
                                                                                                                CssClass="curpointer" hspace="0" ImageAlign="Middle" ImageUrl="~/Images/gicon04.png"
                                                                                                                ToolTip="Delete" vspace="0" OnClick="imgbtnDKeyContact_Click" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <%-- <tr id="ErrorMsg" style="display: block;">
                                                                                                        <td class="error pl10">
                                                                                                            mhihhih
                                                                                                        </td>
                                                                                                    </tr>--%>
                                                                                                    <tr>
                                                                                                        <td>
                                                                                                            <CustomGid:ExtendGrid ID="csKeyContactAttached" runat="server" GridAllowPaging="True"
                                                                                                                GridSelectedRowStyleCSS="BlueViolet" GridShowFooter="False" GridWidth="100%"
                                                                                                                ImageAddButtonEnabled="False" ImageAddButtonURL="/Images/gicon02.png" ImageAdditionalButton1URL="/Images/gicon02.png"
                                                                                                                ImageAdditionalButton2URL="/Images/ArrowRightSmall.png" ImageAdditionalButton3URL="/Images/gicon04.png"
                                                                                                                ImageAdditionalButton4URL="/Images/copy.png" ImageAdditionalButton5URL="/Images/gicon02.png"
                                                                                                                ImageAdditionalButton6URL="/Images/ArrowRightSmall.png" ImageAdditionalButton7URL="/Images/gicon04.png"
                                                                                                                ImageAdditionalButton8URL="/Images/copy.png" ImageAddtionalButton1Enabled="False"
                                                                                                                ImageAddtionalButton2Enabled="False" ImageAddtionalButton3Enabled="False" ImageAddtionalButton4Enabled="False"
                                                                                                                ImageAddtionalButton5Enabled="False" ImageAddtionalButton6Enabled="False" ImageAddtionalButton7Enabled="False"
                                                                                                                ImageAddtionalButton8Enabled="False" ImageCopyButtonEnabled="False" ImageCopyButtonURL="/Images/copy.png"
                                                                                                                ImageDeleteButtonEnabled="False" ImageDeleteButtonURL="/Images/gicon04.png" ImageEditButtonEnabled="False"
                                                                                                                ImageEditButtonURL="/Images/ArrowRightSmall.png" ImageFirstURL="/Images/LeftAllArrow.png"
                                                                                                                ImageLastURL="/Images/RightAllArrow.png" ImageNextURL="/Images/RightArrow.png"
                                                                                                                ImagePreviousURL="/Images/LeftArrow.png" PageNumber="1" ImageAddButtonToolTip="Add"
                                                                                                                ImageCopyButtonToolTip="Copy" ImageDeleteButtonToolTip="Delete" ImageEditButtonToolTip="Edit"
                                                                                                                SortOrder="ASC" OnGridCheckedChange="csKeyContactAttached_GridCheckedChange"
                                                                                                                GridRowIndex="0" />
                                                                                                        </td>
                                                                                                    </tr>
                                                                                                    <asp:Panel ID="pnlKeyAttached" runat="server" Visible="false">
                                                                                                        <tr>
                                                                                                            <td>
                                                                                                                <asp:Label ID="lblRec2" runat="server" Text="No Records to Display!!!"></asp:Label>
                                                                                                            </td>
                                                                                                        </tr>
                                                                                                    </asp:Panel>
                                                                                                </table>
                                                                                            </td>
                                                                                        </tr>
                                                                                    </table>
                                                                                </td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td align="right" valign="middle" class="pr10 greyfooter">
                                                                                </td>
                                                                            </tr>
                                                                        </table>
                                                                    </td>
                                                                </tr>
                                                            </table>
                                                        </ContentTemplate>
                                                    </asp:TabPanel>
                                                </asp:TabContainer>
                                            </td>
                                        </tr>
                                    </table>

                                    <script type="text/javascript" language="javascript">
                                        Sys.WebForms.PageRequestManager.getInstance().add_endRequest(LoadHandler);
                                    </script>

                                    <%--</ContentTemplate>
                            </asp:UpdatePanel>--%>
                                </td>
                            </tr>
                        </table>
                    </td>
                </tr>
                <tr>
                    <td align="right" valign="top" class="pr10 greyfooter">
                        <asp:Button runat="server" ID="btnProjectSave" Text="Save" CssClass="btnstyle" OnClick="btnSave_Click" />
                        <asp:Button runat="server" ID="btnProjectCancel" Text="Cancel" CssClass="btnstyle"
                            OnClientClick="return ConfirmCancel();" OnClick="btnProjectCancel_Click" />
                        <asp:UpdatePanel ID="upsave" runat="server">
                            <ContentTemplate>
                                <asp:Button ID="btnSaveProcess" runat="server" Text="" Style="display: none;" OnClick="btnSaveProcess_Click" />
                            </ContentTemplate>
                        </asp:UpdatePanel>
                    </td>
                </tr>
                <%-- <tr>
            <td align="right" valign="middle" class="pr10 greyfooter" style="height: 40px;" colspan="3">
                <asp:Button ID="btncommitalltab" CssClass="btnstyle" runat="server" Text="Save"
                    OnClick="btncommitalltab_Click" />&nbsp;&nbsp;
                <asp:Button ID="btnCancelalltab" runat="server" CssClass="btnstyle" 
                    Text="Cancel" onclick="btnCancelalltab_Click" />
            </td>
        </tr>--%>
                <tr>
                    <td>
                        <asp:HiddenField ID="hdnfldsPnlUseDfndfld" runat="server" />
                        <asp:HiddenField ID="hdnfldTntSpcInfo" runat="server" />
                        <asp:HiddenField ID="hdnfldSlsContractInfo" runat="server" />
                        <asp:HiddenField ID="hdnfldSalesNewContactInfo" runat="server" />
                        <asp:HiddenField ID="hdnfldTenantNewSpaceNote" runat="server" />
                        <asp:HiddenField ID="hdnfldTenantSort" runat="server" />
                        <asp:HiddenField ID="hdnVendor" runat="server" />
                        <asp:HiddenField ID="hdnRelschUpdate" runat="server" />
                        <asp:HiddenField ID="hdnAuditRpt" runat="server" />
                        <asp:HiddenField ID="hdnNonAccrualStatus" runat="server" />
                        <asp:HiddenField ID="hdnAprisalInfo" runat="server" />
                        <asp:HiddenField ID="hdnNoteNo" runat="server" />
                        <asp:HiddenField ID="hdnUnitNo" runat="server" />
                    </td>
                </tr>
            </table>
            <%--BorrowerInformation--%>
            <%--<asp:ModalPopupExtender ID="mdlBrwinfo" runat="server" TargetControlID="imgbtnBrwinfo"
                PopupControlID="pnlbrwinformation" BackgroundCssClass="modalBackground" CancelControlID="imgbtnClosepopup">--%>
            </asp:ModalPopupExtender>
            <%-- <asp:HoverMenuExtender ID="MouseHowerBrwInfo" runat="server" TargetControlID="lblBrwName" PopupControlID="pnlBrwInfo"
  PopupPosition="Right" >
    </asp:HoverMenuExtender>
 <asp:BalloonPopupExtender ID="BalloonPopupExtender1" runat="server" TargetControlID="lblBrwName2" BalloonPopupControlID="Panel1"
  Position="BottomRight" UseShadow="true"   DisplayOnMouseOver="true" BalloonSize="Large" BalloonStyle="Rectangle" >
    </asp:BalloonPopupExtender> --%>
            <%--BorrowerInformation--%>
            <%--customgrid--%>
            <%-- <asp:ModalPopupExtender ID="MdlPopUpTntSpcInfo" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldTntSpcInfo" PopupControlID="PnlTntSpcInfo" CancelControlID="btnTntSpcInfoCancel">
    </asp:ModalPopupExtender>--%>
            <%--  <asp:ModalPopupExtender ID="MdlPopUseDfndfld" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldsPnlUseDfndfld" PopupControlID="PnlUseDfndfld" CancelControlID="btnUsrDfnFlsCancel">
    </asp:ModalPopupExtender>
    <asp:ModalPopupExtender ID="MdlPopUpSlsContractInfo" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldSlsContractInfo" PopupControlID="PnlSlsContractInfo" CancelControlID="btnSlsCOntractINfoCancel">
    </asp:ModalPopupExtender>
    <asp:ModalPopupExtender ID="MdlPopUpSalesNewContactInfo" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldSalesNewContactInfo" PopupControlID="pnlSalesNewContactInfo"
        CancelControlID="btnNewSalesContractInfoCancel">
    </asp:ModalPopupExtender>
    <asp:ModalPopupExtender ID="MdlPopUpTenantNewSpaceNote" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldTenantNewSpaceNote" PopupControlID="PnlTenantNewSpaceNote"
        CancelControlID="btnTntNewSpaceNoteCancel">
    </asp:ModalPopupExtender>
    <asp:ModalPopupExtender ID="MdlPopUpTenantSort" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnfldTenantSort" PopupControlID="pnlTenantSort" CancelControlID="btnTntSortMdlPopUpCancel">
    </asp:ModalPopupExtender>
    <asp:ModalPopupExtender ID="MdlPopUpasprslfrmMdlpopup" runat="server" BackgroundCssClass="modalBackground"
        TargetControlID="hdnAprisalInfo" PopupControlID="pnlasprslfrmMdlpopup" CancelControlID="btnaprisalCancel">
    </asp:ModalPopupExtender>--%>
            <asp:ModalPopupExtender ID="mdlPopupVendor" runat="server" TargetControlID="hdnVendor"
                PopupControlID="pnlVendor" CancelControlID="btnCancelVendor" BackgroundCssClass="modalBackground">
            </asp:ModalPopupExtender>
            <asp:ModalPopupExtender ID="mdlpopupiframeuserdefined" runat="server" BackgroundCssClass="modalBackground"
                TargetControlID="hdnfldsPnlUseDfndfld" PopupControlID="PnlUseDfndfld" CancelControlID="btnUsrDfnFlsCancel">
            </asp:ModalPopupExtender>
            <asp:ModalPopupExtender ID="mdlPopupRelschUpdate" runat="server" TargetControlID="hdnRelschUpdate"
                PopupControlID="pnlRelschUpdate" CancelControlID="btnCancelRelschUpdate" BackgroundCssClass="modalBackground" />
            <asp:ModalPopupExtender ID="MdlPopUpNonAccrualStatus" runat="server" TargetControlID="hdnNonAccrualStatus"
                PopupControlID="pnlNonAccrualStatus" CancelControlID="btnNonAccrlStatusNo" BackgroundCssClass="modalBackground" />
            <asp:ModalPopupExtender ID="MdlPopUpAuditRpt" runat="server" TargetControlID="hdnAuditRpt"
                PopupControlID="pnlAuditRpt" CancelControlID="btnAdtRptNo" BackgroundCssClass="modalBackground" />
            <asp:Panel ID="PnlUseDfndfld" runat="server" CssClass="mpLarge" Width="65%" Style="display: none">
                <table border="0" cellspacing="" cellpadding="" align="left" width="100%">
                    <tr>
                        <td align="left" valign="middle">
                            <table width="98%" border="0" align="center" cellpadding="0" cellspacing="0">
                                <!-- Table Starts Here -->
                                <tr>
                                    <td align="left" valign="top" width="100%">
                                        <asp:TabContainer ID="tagContainerUsrDfndFld" runat="server" CssClass="Tab" ActiveTabIndex="0">
                                            <asp:TabPanel ID="tabAlphaNumFlds" runat="server">
                                                <HeaderTemplate>
                                                    Alpha-Numeric Fields
                                                </HeaderTemplate>
                                                <ContentTemplate>
                                                    <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                            Alpha-Numeric Fields
                                                                        </td>
                                                                        <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                            <img src="/Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td align="left" valign="top" class="bgcolor6">
                                                                            <table width="100%" border="0" align="center" cellpadding="5" cellspacing="0">
                                                                                <tr>
                                                                                    <td width="24%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                        Origination File Number
                                                                                    </td>
                                                                                    <td width="1%" align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox runat="server" ID="text5303" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                                <tr>
                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                        Acquistion File Number
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox runat="server" ID="text5308" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                                <tr>
                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                        Land Note Number
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox runat="server" ID="text5313" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                            </table>
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                    </table>
                                                </ContentTemplate>
                                            </asp:TabPanel>
                                            <asp:TabPanel ID="tabAmntFlds" runat="server">
                                                <HeaderTemplate>
                                                    Amount Fields
                                                </HeaderTemplate>
                                                <ContentTemplate>
                                                    <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                            Amount Fields
                                                                        </td>
                                                                        <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                            <img src="/Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td align="left" valign="top" class="bgcolor6">
                                                                            <table width="100%" border="0" align="center" cellpadding="5" cellspacing="0">
                                                                                <tr>
                                                                                    <td width="24%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                        Total Closing Costs
                                                                                    </td>
                                                                                    <td width="1%" align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox runat="server" ID="text5344" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                                <tr>
                                                                                    <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                        Invest Reserve Requirement
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox runat="server" ID="text5350" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                            </table>
                                                                        </td>
                                                                    </tr>
                                                                    <tr>
                                                                        <td align="right" valign="top" class="pr10 greyfooter">
                                                                            <asp:Button runat="server" ID="btn5356" CssClass="btnstyle" />
                                                                            &nbsp;&nbsp;<a href="#" class="close"><asp:Button runat="server" ID="btn5357" CssClass="btnstyle" /></a>
                                                                            </a>
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                    </table>
                                                </ContentTemplate>
                                            </asp:TabPanel>
                                            <asp:TabPanel ID="tabDateFlds" runat="server">
                                                <HeaderTemplate>
                                                    Date Fields
                                                </HeaderTemplate>
                                                <ContentTemplate>
                                                    <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                            Date Fields
                                                                        </td>
                                                                        <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                            <img src="/Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td align="left" valign="top">
                                                                <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                                    <tr>
                                                                        <td align="left" valign="top" class="bgcolor6">
                                                                            <table align="center" border="0" cellpadding="5" cellspacing="0" width="100%">
                                                                                <tr>
                                                                                    <td align="left" class="blucolor blackbfont" valign="middle" width="24%">
                                                                                        Servicing Released
                                                                                    </td>
                                                                                    <td align="left" valign="middle" width="1%">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox ID="txtServicingReleased" runat="server" CssClass="txtbox"></asp:TextBox>
                                                                                    </td>
                                                                                </tr>
                                                                                <tr>
                                                                                    <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                        File Audit Date 1
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox ID="txtFileAuditDate1" runat="server" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                                <tr>
                                                                                    <td align="left" class="blucolor blackbfont" valign="middle">
                                                                                        File Audit Date2
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                    </td>
                                                                                    <td align="left" valign="middle">
                                                                                        <asp:TextBox ID="txtFIleAuditDate2" runat="server" CssClass="txtbox" />
                                                                                    </td>
                                                                                </tr>
                                                                            </table>
                                                                        </td>
                                                                    </tr>
                                                                </table>
                                                            </td>
                                                        </tr>
                                                    </table>
                                                </ContentTemplate>
                                            </asp:TabPanel>
                                        </asp:TabContainer>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="right" valign="top" class="pr10 greyfooter">
                                        <asp:Button runat="server" ID="btnUsrDfnFlsOk" Text="OK" CssClass="btnstyle" />
                                        &nbsp;&nbsp;
                                        <asp:Button runat="server" ID="btnUsrDfnFlsCancel" Text="Cancel" CssClass="btnstyle" />
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:Panel ID="pnlVendor" runat="server" CssClass="mpXL" Style="display: none">
                <%--  <asp:UpdatePanel ID="upVendor" runat="server">
            <ContentTemplate>--%>
                <table width="100%" align="center" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td width="100%" height="24px" align="left" valign="middle" class="popupheader">
                            Vendor-Budget Relationships
                        </td>
                    </tr>
                    <tr>
                        <td align="left" valign="top" height="24px" class="bgcolor3">
                            <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                <tr>
                                    <td valign="top">
                                        <table width="100%" border="0" cellspacing="5" cellpadding="0">
                                            <tr>
                                                <td align="left" class="blucolor blackbfont">
                                                    Note Number
                                                </td>
                                                <td align="left" colspan="2">
                                                    &nbsp;&nbsp;&nbsp;<asp:Label ID="lblNoteNumber" runat="server" Text="411"></asp:Label>
                                                </td>
                                                <td class="blucolor blackbfont">
                                                    Unit
                                                </td>
                                                <td colspan="2">
                                                    <asp:Label ID="lblUnit" runat="server" Text="001"></asp:Label>
                                                </td>
                                                <td colspan="2">
                                                    &nbsp;
                                                </td>
                                            </tr>
                                            <tr>
                                                <td align="left" class="blucolor ">
                                                    Vendor Number
                                                </td>
                                                <td align="left" class="blackbfont pl10">
                                                    <asp:TextBox ID="txtVNumber" runat="server" CssClass="txtboxmed"></asp:TextBox>
                                                </td>
                                                <td align="left" width="3%">
                                                    <asp:ImageButton ID="imgbtnSearchVendor" runat="server" ImageUrl="../../Images/gicon01.png"
                                                        vspace="0" hspace="0" border="0" alt="Search Vendor" ImageAlign="Middle" title="Vendor"
                                                        class="curpointer" OnClientClick="javascript:SelectVendor();" ToolTip="Search Vendor" />
                                                    <%-- <img src="../../Images/Vendor.png" alt="Vendor" align="middle" vspace="0" hspace="0" border="0"
                                                        title="Select Vendor" class="curpointer" onclick="javascript:SelectVendor();" />--%>
                                                </td>
                                                <td class="blucolor blackbfont">
                                                    Name
                                                </td>
                                                <td colspan="4">
                                                    <asp:Label ID="lblVName" runat="server" Text="All State" />
                                                </td>
                                            </tr>
                                            <tr>
                                                <td width="12%" class="blucolor blackbfont">
                                                    Address
                                                </td>
                                                <td width="16%">
                                                    <asp:Label ID="lblVAddress1" runat="server" Text="Add1" />
                                                </td>
                                                <td width="12%" class="blucolor blackbfont">
                                                    City
                                                </td>
                                                <td width="12%">
                                                    <asp:Label ID="lblVCity" runat="server" Text="Florida" />
                                                </td>
                                                <td width="12%" class="blucolor blackbfont">
                                                    State
                                                </td>
                                                <td width="12%">
                                                    <asp:Label ID="lblVState" runat="server" Text="TX" />
                                                </td>
                                                <td width="12%" class="blucolor blackbfont">
                                                    Zip
                                                </td>
                                                <td width="12%">
                                                    <asp:Label ID="lblVZip" runat="server" Text="" />
                                                </td>
                                            </tr>
                                            <%--<tr>
                                                <td class="blackbfont">
                                                    Address2
                                                </td>
                                                <td colspan="7">
                                                    <asp:Label ID="lblVAddress2" runat="server" Text="Add2" />
                                                </td>
                                            </tr>--%>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td valign="top">
                                        <CustomGid:ExtendGrid ID="egBudget" runat="server" />
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table width="100%" border="0" cellspacing="8" cellpadding="0">
                                            <tr>
                                                <td>
                                                    <asp:RadioButtonList ID="rbVendorRel" runat="server">
                                                        <asp:ListItem Text="Relate Vendor to the Selected Budget Line Items as Primary Payee"
                                                            Value="0"></asp:ListItem>
                                                        <asp:ListItem Text="Relate Vendor to the Selected Budget Line items as secondary Payee"
                                                            Value="1"></asp:ListItem>
                                                        <asp:ListItem Text="Un-relate Vendor to the selected Budget Line Items" Value="2"></asp:ListItem>
                                                    </asp:RadioButtonList>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td>
                                                    &nbsp;
                                                </td>
                                                <td align="right" valign="middle">
                                                    <asp:Button runat="server" ID="btnApply" Text="Apply" CssClass="btnstyle" />
                                                    &nbsp;&nbsp;<asp:Button runat="server" ID="btnCancelVendor" CssClass="btnstyle" Text="Cancel" />
                                                </td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
                <%--</ContentTemplate>
        </asp:UpdatePanel>--%></asp:Panel>
            <asp:Panel ID="pnlRelschUpdate" runat="server" CssClass="mpXL" Style="display: none">
                <div id="Div1" runat="server" style="max-height: 500px; overflow: auto;">
                    <table width="100%" align="center" cellpadding="1" cellspacing="0" border="0">
                        <tr>
                            <td align="left" valign="middle" height="24px" class="popupheader">
                                Edit Release Schedule
                            </td>
                        </tr>
                        <tr>
                            <td width="100%" align="left" valign="top">
                                <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                    <tr>
                                        <td width="48%" valign="top">
                                            <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                <tr>
                                                    <td valign="top">
                                                        <table align="left" width="100%" cellpadding="0" cellspacing="5px" border="0" class="allborder">
                                                            <tr class="bgcolor4">
                                                                <td height="24px" colspan="3" align="left" valign="middle" class="pl10 blackbfont">
                                                                    Release Information
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td width="171" height="24px" align="left" valign="middle" class="blucolor ">
                                                                    Description
                                                                </td>
                                                                <td width="6" align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td width="151" align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtDescription" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Status
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:CheckBox runat="server" ID="chkStatus" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Minimum Amount
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtMinimumAmount" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Release Date
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtReleaseDate" CssClass="txtbox" Text=" " />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Current Release
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtCurrentRelease" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Last Release
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtLastRelease" CssClass="txtbox" Text=" " />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Paydown Flag
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:CheckBox runat="server" ID="chkPaydownFlag" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td height="24px" colspan="3" align="left" valign="middle">
                                                                    <table width="100%" border="0" align="left" cellpadding="0" cellspacing="5px" class="allborder">
                                                                        <tr class="bgcolor4">
                                                                            <td height="24px" align="left" valign="middle" colspan="3" class="pl10 blackbfont">
                                                                                Sales Information
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                                Amount
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &nbsp;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" class="pl10">
                                                                                <asp:TextBox runat="server" ID="txtAmtSales" CssClass="txtbox" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                                Square Feet
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &nbsp;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" class="pl10">
                                                                                <asp:TextBox runat="server" ID="txtSqFtSales" CssClass="txtbox" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                                Price/Sq feet
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &nbsp;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" class="pl10">
                                                                                <asp:TextBox runat="server" ID="txtPricePerSqFtSales" CssClass="txtbox" />
                                                                            </td>
                                                                        </tr>
                                                                    </table>
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                            </table>
                                        </td>
                                        <td width="3%">
                                            &nbsp;
                                        </td>
                                        <td width="49%" valign="top">
                                            <table width="100%" border="0" cellspacing="0" cellpadding="0">
                                                <tr>
                                                    <td>
                                                        <table width="100%" border="0" align="left" cellpadding="0" cellspacing="5px" class="allborder">
                                                            <tr class="bgcolor4">
                                                                <td height="24px" colspan="3" align="left" valign="middle" class="pl10 blackbfont">
                                                                    Appraisal Information
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Amount
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtAmtAppraisal" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Square Feet
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtSqFtAppraisal" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Price/Sq feet
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtPricePerSqFtAppraisal" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Discounted Amount
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtDiscountedAmt" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class=" ">
                                                                    Type
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:CheckBox runat="server" ID="chkType" name="checkbox3" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Last Appraisal
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtLastAppDate" CssClass="txtbox" Text=" " />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Pct Cmp
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;&nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtPctCmp" CssClass="txtbox" />
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="left" valign="middle" height="24px" class="blucolor ">
                                                                    Last Inspection
                                                                </td>
                                                                <td align="left" valign="middle">
                                                                    &nbsp;
                                                                </td>
                                                                <td align="left" valign="middle" class="pl10">
                                                                    <asp:TextBox runat="server" ID="txtLastInspDate" CssClass="txtbox" Text=" " />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                            </table>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td colspan="3">
                                            <table border="0" cellspacing="1" cellpadding="0" width="100%" align="center" class="allborder">
                                                <tr>
                                                    <td align="left" valign="middle">
                                                        <table border="0" cellspacing="1" cellpadding="5" width="100%" align="center" class="gridheaderbg">
                                                        </table>
                                                    </td>
                                                </tr>
                                                <tr class="bgcolor4">
                                                    <td height="24px" align="left" valign="middle">
                                                        <span class="pl10 blackbfont">Payoff Rules</span>
                                                    </td>
                                                </tr>
                                                <tr>
                                                    <td height="24px" align="left" valign="middle" class="pl10">
                                                        <CustomGid:ExtendGrid ID="egPayoffRules" runat="server" />
                                                    </td>
                                                </tr>
                                            </table>
                                        </td>
                                    </tr>
                                </table>
                            </td>
                        </tr>
                        <tr>
                            <td align="right" valign="middle" height="30px" class="pr10 tborder">
                                <asp:Button runat="server" ID="btnSaveRelschUpdate" CssClass="btnstyle" Text="Save" />
                                &nbsp;&nbsp;<asp:Button runat="server" ID="btnCancelRelschUpdate" CssClass="btnstyle"
                                    Text="Cancel" OnClick="btnCancelRelschUpdate_Click" />
                            </td>
                        </tr>
                    </table>
                </div>
            </asp:Panel>
            <asp:Panel ID="pnlNonAccrualStatus" runat="server" CssClass="mpSmall" Width="45%"
                Style="display: none">
                <table width="100%" align="center" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td align="left" valign="middle" height="24px" class="popupheader">
                            Apply Non-Accrual Status
                        </td>
                    </tr>
                    <tr>
                        <td width="100%" align="left" valign="top">
                            <table border="0" cellspacing="0" cellpadding="0" width="100%" class="allborder">
                                <tr>
                                    <td align="left" valign="top" class="gridheaderbg">
                                        <table border="0" cellspacing="0" cellpadding="5" align="left" width="100%">
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="top">
                                        <table border="0" cellspacing="1" cellpadding="0" width="100%" align="center">
                                            <tr>
                                                <td width="100%" align="left" valign="middle">
                                                    <table width="100%" border="0" cellspacing="8" cellpadding="0">
                                                        <tr>
                                                            <td width="14%" align="left" class="blucolor blackbfont">
                                                                Effective Date
                                                            </td>
                                                            <td width="19%">
                                                                <asp:TextBox runat="server" ID="txtNonAccrlStatusEffctDate" CssClass="txtbox" Text=" YY" />
                                                            </td>
                                                            <td width="67%">
                                                                Loan currently has no 'Open' Interest Receivables
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td colspan="3" align="left">
                                                                Day End Processing will unbook all past due billed interest and all unbilled accrued
                                                                interest.<br />
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td colspan="3" align="left">
                                                                <label for="checkbox">
                                                                    All future billed interest and daily accrual will be carried as 'unbooked'.</label>
                                                            </td>
                                                        </tr>
                                                        <tr>
                                                            <td align="left">
                                                                &nbsp;
                                                            </td>
                                                            <td colspan="2">
                                                                Do you want to continue with implementing the Non-Accrual Status?
                                                            </td>
                                                        </tr>
                                                    </table>
                                                </td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="tborder">
                                        <table border="0" cellspacing="1" cellpadding="5" align="center" width="100%">
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                    <tr>
                        <td align="right" valign="middle" height="30px" class="pr10 tborder">
                            &nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnNonAccrlStatusYes" Text="Yes" CssClass="btnstyle" />&nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnNonAccrlStatusNo" Text="No" CssClass="btnstyle" />
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:Panel ID="pnlAuditRpt" runat="server" CssClass="mpSmall" Width="65%" Style="display: none">
                <table width="100%" align="center" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td align="left" valign="middle" height="24px" class="popupheader">
                            Audit Report
                        </td>
                    </tr>
                    <tr>
                        <td width="100%" align="left" valign="top">
                            <table border="0" cellspacing="0" cellpadding="0" width="100%" class="allborder">
                                <tr>
                                    <td align="left" valign="top" class="gridheaderbg">
                                        <table border="0" cellspacing="0" cellpadding="5" align="left" width="100%">
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="top">
                                        <table border="0" cellspacing="1" cellpadding="0" width="100%" align="center">
                                            <tr>
                                                <td width="100%" align="left" valign="middle">
                                                    <table width="100%" border="0" cellspacing="8" cellpadding="0">
                                                        <tr>
                                                            <td align="left">
                                                                <label for="textarea">
                                                                </label>
                                                                <textarea name="textarea" rows="12" id="textarea" style="width: 95%">Note 121FGF14 001 contains the following Potential Issues


                        Legal description is missing

                        Budget Estimated $0.00 - Allocated$7,000.00 = ($7,000.00)

                        Interest Profile or Interest Rate Missing

                        Interest Profile or Billing Cycle Missing</textarea>
                                                                <br />
                                                            </td>
                                                        </tr>
                                                    </table>
                                                </td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="tborder">
                                        <table border="0" cellspacing="1" cellpadding="5" align="center" width="100%">
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                    <tr>
                        <td align="right" valign="middle" height="30px" class="pr10 tborder">
                            &nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnAdtRptYes" Text="Yes" CssClass="btnstyle" />&nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnAdtRptNo" Text="No" CssClass="btnstyle" />
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <%--  <asp:UpdatePanel ID="UpLIProfile" runat="server" UpdateMode="Conditional">
        <ContentTemplate>--%>
            <asp:HiddenField ID="hdnHide1" runat="server" />
            <asp:ModalPopupExtender ID="popupLIProfile" runat="server" PopupControlID="pnlLIProfile"
                TargetControlID="hdnHide1" BackgroundCssClass="modalBackground">
            </asp:ModalPopupExtender>
            <asp:Panel ID="pnlLIProfile" runat="server" CssClass="mpXL" Style="display: none">
                <table width="98%" border="0" align="center" cellpadding="0" cellspacing="0">
                    <!-- Table Starts Here -->
                    <tr>
                        <td align="left" valign="middle" class="blackbfont" height="27px">
                            New: Line of Credit Interest Profile -
                        </td>
                    </tr>
                    <tr>
                        <td align="left" valign="top" width="100%">
                            <asp:TabContainer ID="TabContainer1" runat="server" ActiveTabIndex="1" CssClass="Tab">
                                <asp:TabPanel ID="TabPanel2" runat="server">
                                    <HeaderTemplate>
                                        General Rate Options
                                    </HeaderTemplate>
                                    <ContentTemplate>
                                        <div id="Div4">
                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                            <tr>
                                                                <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                    General Rate Options
                                                                </td>
                                                                <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                    <img src="../../Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                            <tr>
                                                                <td align="left" valign="top" class="bgcolor6">
                                                                    <table width="100%" border="0" align="center" cellpadding="5" cellspacing="0">
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Rate Type
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" colspan="4">
                                                                                <select name="slct" id="Select4" onchange="rohan(this.value)" class="ddlistbox">
                                                                                    <option>Select</option>
                                                                                    <option value="1">Fixed Rate</option>
                                                                                    <option value="2">Variable Rate - VRM</option>
                                                                                    <option value="3">Adjustable Rate - ARM</option>
                                                                                </select>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Number of Days - Yearly
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="25%" align="left" valign="middle">
                                                                                <select name="category" id="Select5" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>360</option>
                                                                                    <option>365 365365</option>
                                                                                    <option>366 366366</option>
                                                                                </select>
                                                                            </td>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Actual Days - Monthly
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="*" align="left" valign="middle">
                                                                                <select name="category2" id="Select6" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>Actual</option>
                                                                                    <option>30 Days</option>
                                                                                </select>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="pl10 blackbfont" colspan="6">
                                                                                Rates
                                                                            </td>
                                                                        </tr>
                                                                        <tr id="Tr1">
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Fixed Rate
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" colspan="4">
                                                                                <select name="category" id="Select7" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>000-Prime</option>
                                                                                    <option>001-List</option>
                                                                                </select><a href="#" class="close"><input type="button" class="btnstyle" value="View" /></a>
                                                                            </td>
                                                                        </tr>
                                                                        <tr id="Tr2">
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Fixed Rate
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input class="txtbox" type="text" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Default Rate
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input class="txtbox" type="text" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Effective Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input class="txtbox" type="text" value="DD/MM/YYYY" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Maturity Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input class="txtbox" type="text" value="DD/MM/YYYY" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Review Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&#160;
                                                                            </td>
                                                                            <td align="left" valign="middle" colspan="4">
                                                                                <input type="text" class="txtbox" value="DD/MM/YYYY" />
                                                                            </td>
                                                                        </tr>
                                                                    </table>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="right" valign="middle" class="pl10 greyfooter">
                                                                    <asp:Button ID="Button1" runat="server" Text="OK" CssClass="btnstyle" />&nbsp;<asp:Button
                                                                        ID="btnCancelLiprofile" runat="server" CssClass="btnstyle" Text="Cancel" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                            </table>
                                        </div>
                                    </ContentTemplate>
                                </asp:TabPanel>
                                <asp:TabPanel ID="TabPanel3" runat="server">
                                    <HeaderTemplate>
                                        Additional Rate Information
                                    </HeaderTemplate>
                                    <ContentTemplate>
                                        <div id="Div2">
                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                            <tr>
                                                                <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                    Additional Rate Information
                                                                </td>
                                                                <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                    <img src="../../Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                            <tr>
                                                                <td align="left" valign="top" class="bgcolor6">
                                                                    <table width="100%" border="0" align="center" cellpadding="5" cellspacing="0">
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="pl10 blackbfont" colspan="6">
                                                                                Variable Rate Information
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Margin
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="25%" align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Dft Margin
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="*" align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Life Cap
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" disabled="disabled" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Floor
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Ceiling
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Adj. Cap
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Rounding
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                                <asp:Button ID="btnRoundPnl" runat="server" Text=".." CssClass="btnstyle" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Interest Rate
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="pl10 blackbfont" colspan="6">
                                                                                Adjustable Rate Information
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor pl10">
                                                                                Prime Eff. Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="DD/MM/YYYY" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Next Eff. Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="DD/MM/YYYY" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Freq. Factor
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Freq. Factor
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Method
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Method
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Adj.
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Adj.
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Days
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Days
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                    </table>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="right" valign="middle" class="pl10 greyfooter">
                                                                    <a href="#" class="close">
                                                                        <input type="button" class="btnstyle" value="OK" /></a>
                                                                    <asp:Button ID="btnLIP2" runat="server" Text="Cancel" CssClass="btnstyle" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                            </table>
                                        </div>
                                    </ContentTemplate>
                                </asp:TabPanel>
                                <asp:TabPanel ID="TabPanel4" runat="server">
                                    <HeaderTemplate>
                                        Billing Options
                                    </HeaderTemplate>
                                    <ContentTemplate>
                                        <div id="Div3">
                                            <table width="100%" class="allgborder" cellpadding="1" cellspacing="0" border="0">
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                                            <tr>
                                                                <td width="*" align="left" valign="middle" class="pl10 bbggridhead tablehdfont dotbtborder">
                                                                    Billing Options
                                                                </td>
                                                                <td width="110px" height="35px" align="right" valign="top" class="dotbtborder">
                                                                    <img src="../../Images/yobg.png" border="0" vspace="0" hspace="0" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                                <tr>
                                                    <td align="left" valign="top">
                                                        <table width="100%" align="center" cellpadding="5" cellspacing="0" border="0">
                                                            <tr>
                                                                <td align="left" valign="top" class="bgcolor6">
                                                                    <table width="100%" border="0" align="center" cellpadding="5" cellspacing="0">
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Cycle
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <select name="category" id="Select8" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>360</option>
                                                                                    <option>365</option>
                                                                                    <option>366</option>
                                                                                </select>
                                                                            </td>
                                                                            <td align="left" valign="middle" class=" blackbfont" colspan="3">
                                                                                Late Fees
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Day
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="25%" align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td width="20%" align="left" valign="middle" class="blucolor blackbfont">
                                                                                Days
                                                                            </td>
                                                                            <td width="1%" align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td width="*" align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Next
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="DD/MM/YYYY" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Amount
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Fixed P&amp;I Amount
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Percentage
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Next P&amp;I Date
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="DD/MM/YYYY" />
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Min. % Amount
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="pl10">
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Max. % Amount
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <input type="text" class="txtbox" value="" />
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Bill Method
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle" colspan="4">
                                                                                <select name="category2" id="Select9" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>Bill</option>
                                                                                    <option>Auto-Detect</option>
                                                                                </select>
                                                                            </td>
                                                                        </tr>
                                                                        <tr>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Auto-Detect
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <select name="category3" id="Select10" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>Commitment</option>
                                                                                    <option>Deposit</option>
                                                                                    <option>Escrow</option>
                                                                                </select>
                                                                            </td>
                                                                            <td align="left" valign="middle" class="blucolor blackbfont">
                                                                                Line Item
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                &#160;&nbsp;
                                                                            </td>
                                                                            <td align="left" valign="middle">
                                                                                <select name="category4" id="Select11" class="ddlistbox">
                                                                                    <option selected="selected">Select</option>
                                                                                    <option>Note Level</option>
                                                                                    <option>Type Line-Item ID</option>
                                                                                </select>
                                                                            </td>
                                                                        </tr>
                                                                    </table>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td align="right" valign="middle" class="pl10 greyfooter">
                                                                    <input type="button" class="btnstyle" value="OK" />
                                                                    <asp:Button ID="btnCancelLIP3" runat="server" Text="Cancel" CssClass="btnstyle" />
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </td>
                                                </tr>
                                            </table>
                                        </div>
                                    </ContentTemplate>
                                </asp:TabPanel>
                            </asp:TabContainer>
                        </td>
                    </tr>
                    <!-- Table Ends Here -->
                </table>
            </asp:Panel>
            <asp:HiddenField ID="hdnHide2" runat="server" />
            <asp:ModalPopupExtender ID="popupRoundOption" runat="server" PopupControlID="PnlRoundOption"
                TargetControlID="hdnHide2" BackgroundCssClass="modalBackground">
            </asp:ModalPopupExtender>
            <asp:Panel ID="PnlRoundOption" runat="server" CssClass="mpSmall" Style="display: none">
                <table border="0" cellspacing="0" cellpadding="0" align="left" width="100%">
                    <tr>
                        <td align="left" valign="middle">
                            <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                <tr>
                                    <td align="left" valign="middle" class="popupheader">
                                        Select Rounding Option
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle">
                                        <table width="100%" align="left" cellpadding="0" cellspacing="0" border="0">
                                            <tr>
                                                <td align="left" valign="middle" class="pl10">
                                                    <asp:RadioButtonList ID="rdRound" runat="server">
                                                        <asp:ListItem Text="Up" Value="0"></asp:ListItem>
                                                        <asp:ListItem Text="Down" Value="1"></asp:ListItem>
                                                        <asp:ListItem Text="Nearest" Value="2"></asp:ListItem>
                                                    </asp:RadioButtonList>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td align="left" valign="middle">
                                                    <asp:DropDownList ID="ddlRound" runat="server" AutoPostBack="true">
                                                        <asp:ListItem Value="0" Text="Select"></asp:ListItem>
                                                        <asp:ListItem Value="1" Text="Half"></asp:ListItem>
                                                        <asp:ListItem Value="2" Text="Hole"></asp:ListItem>
                                                        <asp:ListItem Value="3" Text="Quarter"></asp:ListItem>
                                                        <asp:ListItem Value="4" Text="Eighth"></asp:ListItem>
                                                    </asp:DropDownList>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td>
                                                    <asp:RadioButton ID="rdRoundOther" runat="server" Text="Other" AutoPostBack="true" />
                                                    <asp:TextBox ID="txtRoundOther" runat="server" CssClass="txtbox"></asp:TextBox>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td>
                                                    <asp:Panel ID="pnlOther" runat="server">
                                                        <asp:Label ID="lblOther" runat="server" Text="The Other Rounding Option is for rounding up"></asp:Label>
                                                    </asp:Panel>
                                                    <asp:Panel ID="pnlGroup" runat="server" Visible="false">
                                                        <table>
                                                            <tr>
                                                                <td align="left" valign="middle" class="popupheader" colspan="3">
                                                                    Rounding Result
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>
                                                                    <asp:Label ID="lblRate" runat="server" Text="Rate : 0.00%"></asp:Label>
                                                                </td>
                                                                <td>
                                                                    <asp:Label ID="lblMarign" runat="server" Text="Margin : 0.00%"></asp:Label>
                                                                </td>
                                                                <td>
                                                                    <asp:Label ID="lblRounding" runat="server" Text="No Rounding : 0.000%"></asp:Label>
                                                                </td>
                                                            </tr>
                                                        </table>
                                                    </asp:Panel>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td align="right" height="30px" valign="middle" class="pr20 greyfooter">
                                                    <%--<a href="#EditUser1" name="modal" id="A11"><input type="button" value="Ok" class="btnstyle" />
                                </a>--%>
                                                    <asp:Button ID="btnRoundSave" runat="server" Text="OK" CssClass="btnstyle" />&nbsp;
                                                    <asp:Button ID="btnCancelRound" runat="server" Text="Cancel" class="btnstyle" />
                                                </td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:HiddenField ID="hdnIPEffDate" runat="server" />
            <asp:HiddenField ID="hdnEPEQtype" runat="server" />
            <asp:HiddenField ID="hdnEPEffDate" runat="server" />
            <asp:HiddenField ID="hdnEPBudgetID" runat="server" />
            <asp:HiddenField ID="hdnAttachDetails" runat="server" />
            <asp:ModalPopupExtender ID="mPopupAttachdetails" runat="server" TargetControlID="hdnAttachDetails"
                PopupControlID="pnlAttachDetails" BackgroundCssClass="modalBackground" CancelControlID="btnCancel018" />
            <asp:Panel ID="pnlAttachDetails" runat="server" CssClass="mpMedium" Style="display: none">
                <table border="0" cellspacing="0" cellpadding="0" align="left" width="100%">
                    <tr>
                        <td align="left" valign="middle">
                            <table width="100%" align="left" cellpadding="0" cellspacing="2" border="0">
                                <tr>
                                    <td>
                                        <table border="0" cellpadding="0" cellspacing="0" width="100%" class="allborder">
                                            <tr>
                                                <td align="left" valign="middle" height="24px" class="popupheader" colspan="3">
                                                    Document Details
                                                </td>
                                            </tr>
                                            <tr class="normalrow">
                                                <td width="25%" height="24px" align="left" valign="middle" class="blucolor pl10">
                                                    Note
                                                </td>
                                                <td width="1%" height="24px" align="left" valign="middle">
                                                </td>
                                                <td width="80%" height="24px" align="left" valign="middle">
                                                    <asp:Label ID="lblNoteInfo" runat="server" CssClass="lblRight" />
                                                </td>
                                            </tr>
                                            <tr class="first altrow">
                                                <td width="19%" height="24px" align="left" valign="middle" class="blucolor pl10">
                                                    Attached
                                                </td>
                                                <td width="1%" height="24px" align="left" valign="middle">
                                                </td>
                                                <td width="80%" height="24px" align="left" valign="middle">
                                                    <asp:Label ID="lblAttached" runat="server" CssClass="lblRight" />
                                                </td>
                                            </tr>
                                            <tr class="normalrow">
                                                <td height="24px" align="left" valign="middle" class="blucolor pl10">
                                                    Attachment ID
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                    <asp:Label ID="lblAttachID" runat="server" CssClass="lblRight" />
                                                </td>
                                            </tr>
                                            <tr class="first altrow">
                                                <td height="24px" align="left" valign="middle" class="blucolor pl10">
                                                    Description
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                    <asp:Label ID="lblDescription" runat="server" CssClass="lblRight" />
                                                </td>
                                            </tr>
                                            <%--<tr class="normalrow">
                                                <td height="24px" align="left" valign="middle" class="blucolor pl10">
                                                    File Location
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                </td>
                                                <td height="24px" align="left" valign="middle">
                                                    <asp:Label ID="lblFileLocation" runat="server" CssClass="lblRight" />
                                                </td>
                                            </tr>--%>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="right" valign="middle" height="30px" class="pr10 tborder">
                                        <asp:Button runat="server" ID="btnOk018" Text="OK" CssClass="btnstyle" />
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:HiddenField ID="hdnAttachDoc" runat="server" />
            <asp:ModalPopupExtender ID="mPopupAttachDoc" runat="server" TargetControlID="hdnAttachDoc"
                PopupControlID="pnlAttachDoc" BackgroundCssClass="modalBackground" />
            <asp:UpdatePanel ID="docPanel1" runat="server">
                <ContentTemplate>
                    <asp:Panel ID="pnlAttachDoc" runat="server" CssClass="mpLarge" Style="display: none">
                        <table width="99%" align="center" cellpadding="1" cellspacing="0" border="0" style="display: block">
                            <tr id="trValidsumm" runat="server">
                                <td align="left" valign="middle">
                                    <asp:ValidationSummary class="ErrorSummary" ID="ValidationSummaryAttachments" runat="server"
                                        ValidationGroup="Attachment" ShowSummary="true" />
                                </td>
                            </tr>
                        </table>
                        <table width="99%" align="center" cellpadding="1" cellspacing="0" border="0">
                            <tr>
                                <td align="left" valign="middle" height="24px" class="pl5 bgcolor4 blackbfont">
                                    Attach Document
                                </td>
                            </tr>
                            <tr>
                                <td width="100%" align="left" valign="top">
                                    <table align="left" width="100%" cellpadding="1" cellspacing="0" border="0" class="allborder">
                                        <tr>
                                            <td height="24px" align="left" valign="middle" class="blucolor">
                                                Enter the path and filename of the document you want to attach<span class="colorerr">*</span>
                                            </td>
                                            <td width="10" align="left" valign="middle">
                                            </td>
                                            <td align="left" valign="middle">
                                                <asp:FileUpload ID="fuAttachments" runat="server" Width="330px" />
                                                <asp:RequiredFieldValidator ID="reqFlValAttach" runat="server" ValidationGroup="Attachment"
                                                    ControlToValidate="fuAttachments" Display="None" ErrorMessage="Please select a record to attach." />
                                            </td>
                                        </tr>
                                        <tr>
                                            <td align="left" valign="middle" class="blucolor">
                                                Document Description
                                            </td>
                                            <td width="10" align="left" valign="middle">
                                            </td>
                                            <td align="left" valign="top">
                                                <asp:TextBox ID="txtDocument" runat="server" CssClass="txtboxMultiLine" TextMode="MultiLine"
                                                    onkeyDown="return checkTextAreaMaxLength(this,event,'250');" />
                                            </td>
                                        </tr>
                                    </table>
                                </td>
                            </tr>
                            <tr>
                                <td align="right" valign="middle" height="30px">
                                    <asp:Button ID="btnAttachmentOk" runat="server" Text="OK" CssClass="btnstyle" ValidationGroup="Attachment"
                                        OnClick="btnAttachmentOk_Click" />
                                    &nbsp;&nbsp;
                                    <asp:Button ID="btnAttachmentCancel" runat="server" Text="Cancel" CssClass="btnstyle" />
                                </td>
                            </tr>
                        </table>
                    </asp:Panel>
                </ContentTemplate>
            </asp:UpdatePanel>
            <asp:HiddenField ID="hdnAddBudget" runat="server" />
            <asp:ModalPopupExtender ID="mpeAddBudget" runat="server" TargetControlID="hdnAddBudget"
                PopupControlID="pnlAddBudget" BackgroundCssClass="modalBackground" CancelControlID="btnBudgetCancel" />
            <asp:Panel ID="pnlAddBudget" runat="server" CssClass="mpMedium" Style="display: none">
                <table width="100%" align="center" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td align="left" valign="middle" height="24px" class="popupheader" colspan="6">
                            Budget Insert
                        </td>
                    </tr>
                    <tr>
                        <td height="24px" align="left" valign="middle" class="blucolor pl10">
                            Note:
                        </td>
                        <td align="left" valign="left">
                        </td>
                        <td align="left" valign="left" class="pl10">
                            <asp:Label ID="lblNoteNo" runat="server"></asp:Label>
                        </td>
                        <td align="left" valign="left" class="pl10">
                            &nbsp;
                        </td>
                    </tr>
                    <tr>
                        <td height="24px" align="left" valign="middle" class="blucolor pl10">
                            Unit:
                        </td>
                        <td align="left" valign="left">
                        </td>
                        <td align="left" valign="left" class="pl10">
                            <asp:Label ID="lblUnitNumber" runat="server"></asp:Label>
                        </td>
                        <td align="left" valign="left" class="pl10">
                            &nbsp;
                        </td>
                    </tr>
                    <tr>
                        <td height="24px" align="left" valign="middle" class="blucolor pl10">
                            ID:
                        </td>
                        <td align="left" valign="left">
                        </td>
                        <td colspan="2" align="left" valign="left" class="pl10">
                            <asp:Label ID="lblBudgetId" runat="server"></asp:Label>
                        </td>
                    </tr>
                    <tr>
                        <td width="25%" height="24px" align="left" valign="middle" class="blucolor pl10">
                            Group ID
                        </td>
                        <td width="1%" align="left" valign="left">
                        </td>
                        <td width="15%" align="left" valign="left" class="pl10">
                            <asp:TextBox runat="server" ID="txtGroupID" CssClass="txtbox" MaxLength="2" />
                        </td>
                        <td width="*" align="left" valign="left" class="pl10">
                            &nbsp;
                        </td>
                    </tr>
                    <tr>
                        <td align="left" valign="middle" height="24px" class="blucolor pl10">
                            Description
                        </td>
                        <td align="left" valign="middle">
                        </td>
                        <td align="left" valign="middle" class="pl10" colspan="2">
                            <asp:TextBox runat="server" ID="txtGroupDesc" CssClass="txtbox" MaxLength="50" />
                        </td>
                    </tr>
                    <tr>
                        <td align="right" valign="middle" height="30px" class="pr10 tborder" colspan="6">
                            <asp:Button runat="server" ID="btnAddBudgetOK" Text="OK" CssClass="btnstyle" OnClick="btnAddBudget_Click"
                                OnClientClick="return IsGroupEmpty();" />&nbsp;&nbsp;
                            <asp:Button ID="btnBudgetCancel" runat="server" Text="Cancel" CssClass="btnstyle" />
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:ModalPopupExtender ID="mpopupDocAdd" runat="server" TargetControlID="hdnDocAdd"
                PopupControlID="pnlDocAdd" BackgroundCssClass="modalBackground" CancelControlID="btnDocCancel" />
            <asp:Panel ID="pnlDocAdd" runat="server" CssClass="mpMedium" Style="display: none">
                <table width="100%" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td align="left" valign="middle" height="24px" class="popupheader">
                            Document Insert
                        </td>
                    </tr>
                    <tr>
                        <td width="100%" align="left" valign="top">
                            <table align="left" width="100%" cellpadding="0" cellspacing="8" border="0" class="allborder">
                                <tr>
                                    <td colspan="3">
                                        <table align="left" width="100%" cellpadding="0" cellspacing="8" border="0" class="allgborder">
                                            <tr>
                                                <td align="left" valign="middle" class="blucolor pl10" style="width: 5%">
                                                    Note:
                                                </td>
                                                <td align="left" style="width: 45%">
                                                    <asp:Label runat="server" ID="lblDocNoteNo"></asp:Label>
                                                </td>
                                                <td align="left" valign="middle" class="blucolor pl10" style="width: 5%">
                                                    Unit:
                                                </td>
                                                <td align="left" style="width: 45%">
                                                    <asp:Label runat="server" ID="lblDocUnit"></asp:Label>
                                                </td>
                                            </tr>
                                            <tr>
                                                <td align="left" valign="middle" class="blucolor pl10">
                                                    ID
                                                </td>
                                                <td align="left">
                                                    <asp:Label runat="server" ID="lblDocId"></asp:Label>
                                                </td>
                                                <td align="left" valign="middle" class="pl10">
                                                </td>
                                                <td align="left" valign="middle">
                                                </td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="blucolor pl10">
                                        Group ID
                                    </td>
                                    <td width="18" align="left" valign="middle">
                                    </td>
                                    <td align="left" valign="middle" class="pl10">
                                        <asp:TextBox runat="server" ID="txtDocGroupId" CssClass="txtbox" MaxLength="2" />
                                        <asp:FilteredTextBoxExtender ID="FilteredTextBoxExtender15" runat="server" TargetControlID="txtGroupId"
                                            FilterType="Numbers" Enabled="True" />
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="blucolor pl10">
                                        Priority
                                    </td>
                                    <td align="left" valign="middle">
                                    </td>
                                    <td align="left" valign="middle" class="pl10">
                                        <asp:TextBox runat="server" ID="txtPri" CssClass="txtbox" Text="" MaxLength="2" Width="43px" />
                                        <asp:FilteredTextBoxExtender ID="txtPri_FilteredTextBoxExtender1" runat="server"
                                            TargetControlID="txtPri" FilterType="Numbers" Enabled="True" />
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="blucolor pl10">
                                        Number of Days
                                    </td>
                                    <td align="left" valign="middle">
                                    </td>
                                    <td align="left" valign="middle" class="pl10">
                                        <asp:TextBox runat="server" ID="txtBorDays" CssClass="txtbox" Text="" MaxLength="3"
                                            Height="16px" Width="43px" />
                                        <asp:FilteredTextBoxExtender ID="txtBorDays_FilteredTextBoxExtender1" runat="server"
                                            TargetControlID="txtBorDays" FilterType="Numbers" Enabled="True" />
                                    </td>
                                </tr>
                                <tr>
                                    <td align="left" valign="middle" class="blucolor pl10">
                                        Description
                                    </td>
                                    <td align="left" valign="middle">
                                    </td>
                                    <td align="left" valign="middle" class="pl10">
                                        <asp:TextBox ID="txtDocDesc" runat="server" TextMode="MultiLine" Width="278px" />
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                    <tr>
                        <td align="right" valign="middle" height="30px" class="pr10 tborder">
                            <asp:Button runat="server" ID="btnDocIdMain" Text="OK" CssClass="btnstyle" OnClick="btnSaveDoc_Click"
                                OnClientClick="return CheckDoc();" />&nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnDocCancel" Text="Cancel" CssClass="btnstyle" />
                        </td>
                    </tr>
                </table>
            </asp:Panel>
            <asp:HiddenField ID="hdnDocEdit" runat="server" />
            <asp:HiddenField ID="hdnDocAdd" runat="server" />
            <asp:HiddenField ID="hdnDocId" runat="server" />
            <asp:HiddenField ID="hdnInquiry" runat="server" />
            <%--  <asp:HiddenField ID="hdnRelSch" runat="server" />
             <asp:ModalPopupExtender ID="mdlPopupRelSchdle" runat="server" TargetControlID="hdnRelSch"
                PopupControlID="pnlRelSchdle" BackgroundCssClass="modalBackground" CancelControlID="btnRelSchdleCancelPopup" />
            <asp:Panel ID="pnlRelSchdle" runat="server" CssClass="mpSmall" Style="display: none">
                <table width="100%" cellpadding="1" cellspacing="0" border="0">
                    <tr>
                        <td align="left" valign="middle" height="24px" class="popupheader">
                            Release Schedule
                        </td>
                    </tr>
                    <tr>
                        <td width="100%" align="left" valign="top">
                            <table align="left" width="100%" cellpadding="0" cellspacing="8" border="0" class="allborder">
                                <tr> <td>
                                <asp:RadioButtonList ID="rdReleaseSchedule" runat="server">
                                <asp:ListItem Text="Single record Edit" Value="0" Selected="True"></asp:ListItem>
                                <asp:ListItem Text="Multi record Edit" Value="1"></asp:ListItem>
                                </asp:RadioButtonList>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                    <tr>
                        <td align="right" valign="middle" height="30px" class="pr10 tborder">
                            <asp:Button runat="server" ID="btnRelSchdleOKPopup" Text="OK" CssClass="btnstyle" OnClick="btnRelSchdleOKPopup_Click" />&nbsp;&nbsp;
                            <asp:Button runat="server" ID="btnRelSchdleCancelPopup" Text="Cancel" CssClass="btnstyle" />
                        </td>
                    </tr>
                </table>
            </asp:Panel>--%>
        </ContentTemplate>
        <Triggers>
            <asp:PostBackTrigger ControlID="btnAttachmentOk" />
        </Triggers>
    </asp:UpdatePanel>

    <script language="javascript" type="text/javascript">
        //Save Start

        function CheckDoc() {
            var vDesc = $("#<%= txtDocDesc.ClientID %>").val();
            if (vDesc == '') {
                alert('Please enter a description.');
                return false;
            }

        }
        var btnBackendSave = '<%= btnSaveProcess.ClientID %>';
        function Save1(mProp_Inquiry, adminFlag, noteAction, bRenewal, noteMode, nRenewalCount, dPrevMatDate, dPrvCompDate) {
            var bFeePostCompDate;
            var bFeePostMaturity;
            if (mProp_Inquiry == true) {
                return false;
            }

            if (confirm("Are you sure you want to save note edits?") == false) {
                return false;
            }

            var chkRevolving = document.getElementById('<%= chkRevolving.ClientID %>');
            var chkForeclosure = document.getElementById('<%= chkForeclosure.ClientID %>');
            var btnSave = document.getElementById('<%= btnProjectSave.ClientID %>');
            var tbNoteInfo = null;
            if (chkRevolving.checked == true && chkForeclosure.checked == true) {
                alert("This loan is flagged as FannieMae and should not revolve.");
                SetActiveTab(1); //General TAB
                chkRevolving.checked = false;
                chkRevolving.disabled = true;

                if (btnSave.disabled == false) {
                    btnSave.focus();
                    return false;
                }
            } //PASSED

            var drpdwnlstAdmin = document.getElementById('<%= drpdwnlstAdmin.ClientID %>');
            if (adminFlag == "Y" && drpdwnlstAdmin.value == "") {
                tbNoteInfo.ActiveTab = 0; // Project Tab
                alert("Please Assign the Administrator associated for this record");
                drpdwnlstAdmin.focus();
                return false;
            } //PASSED

            var txtDateTabMturty = document.getElementById('<%= txtDateTabMturty.ClientID %>');
            var sRenewal;
            if (noteAction == 2 && bRenewal == false && noteMode != "PIPELINE") {
                if (ConvertToDateTime(dPrevMatDate) != ConvertToDateTime(txtDateTabMturty.value)) {
                    bRenewal = true;
                    bFeePostMaturity = 0;
                    if (confirm("Are you renewing this note?", "Maturity Date Change") == true) {
                        sRenewal = "Loan Renewal";
                        nRenewalCount += 1;

                        if (confirm("Do you want to post a Renewal Fee?", "Fee Posting") == true) {
                            bFeePostMaturity = -1;
                        }
                    }
                    else {
                        sRenewal = "Maturity Date Changed";
                    }
                }
            }

            //alert(chkFannieMae.checked + ": Checked");
            //alert(dPrvCompDate + ": dPrvCompDate");
            if (dPrvCompDate != "") {
                /*NEED TO FIX BELOW LINE*/
                var dateOne = new Date(dPrvCompDate);
                var txtDateTabCnsCmpl = new Date(document.getElementById('<%= txtDateTabCnsCmpl.ClientID %>').value);
                if (dateOne < txtDateTabCnsCmpl && DateDiff(dPrvCompDate, txtDateTabCnsCmpl) > 0) {
                    if (confirm("Do you want to post an Extension Fee?") == true) {
                        bFeePostCompDate = -1;
                    }
                }
            }

            this.document.forms[0].__EVENTTARGET.value = "{\"bFeePostCompDate\":\"" + bFeePostCompDate + "\",\"bFeePostMaturity\":\"" + bFeePostMaturity + "\",\"nRenewalCount\":\"" + nRenewalCount + "\",\"bRenewal\":\"" + bRenewal + "\"}";
            this.document.forms[0].__EVENTARGUMENT.value = "save1";
            document.getElementById(btnBackendSave).click();
            //raise button click for save cont..with values.
        }

        function DateDiff(dtFrom, dtTo) {
            var dt1 = new Date(dtFrom);
            var dt2 = new Date(dtTo);
            var diff = dt2.getTime() - dt1.getTime();
            var days = diff / (1000 * 60 * 60 * 24);
            return days;
        }

        function ConvertToDateTime(dateVal) {
            var myDate = dateVal;
            var regExp = /(\d{1,2})\/(\d{1,2})\/(\d{2,4})/;
            return myDate.replace(regExp, "$3$1$2");
        }

        function Save2(cEst, cAlloc) {
            var cDiff = "";
            if (cEst != cAlloc) {
                cDiff = cEst - cAlloc;
                var sMsg = "Budget fields 'Total Estimated' and 'Total Allocated' do not equal!" + "\n" + "This may cause problems with funding and balancing your loan budget." + "\n" + "\n" + "Continue and Exit anyway?";
                sMsg = sMsg + "\r" + "\r" + "Press YES to continue, NO to modify.";
                if (confirm(sMsg) == false) {
                    cAlloc = 0;
                    cEst = 0;
                    SetActiveTab(5); //tbNoteInfo.ActiveTab = GetTabIndex("FINANCIALS"); // 5
                    return false;
                }
                else {
                    this.document.forms[0].__EVENTTARGET.value = "{\"cDiff\":\"" + cDiff + "\",\"cEst\":\"" + cEst + "\",\"cAlloc\":\"" + cAlloc + "\"}";
                    this.document.forms[0].__EVENTARGUMENT.value = "save2";
                    document.getElementById(btnBackendSave).click();
                    return false;
                }
            }
            else {
                this.document.forms[0].__EVENTTARGET.value = "{\"cDiff\":\"" + cDiff + "\",\"cEst\":\"" + cEst + "\",\"cAlloc\":\"" + cAlloc + "\"}";
                this.document.forms[0].__EVENTARGUMENT.value = "save2";
                document.getElementById(btnBackendSave).click();
                return false;
            }
        }

        function Save3(dblFincTabprincBal3, dblFincTabLoanCommit3) {
            //alert("dblFincTabprincBal3=" + dblFincTabprincBal3 + ":  dblFincTabLoanCommit3=" + dblFincTabLoanCommit3);
            if ((dblFincTabprincBal3 > dblFincTabLoanCommit3) || dblFincTabprincBal3 < 0) {
                alert("Invalid amount.  The Principal Balance Cap cannot exceed the Loan Commitment amount nor can it be a negative amount.");
                SetActiveTab(5); //tbNoteInfo.ActiveTab = GetTabIndex("FINANCIALS");
                var txtFincTabprincBal2 = document.getElementById('<%= txtFincTabprincBal2.ClientID %>');
                if (txtFincTabprincBal2.disabled == false) {
                    txtFincTabprincBal2.focus();
                }
                return false;
            }
            else {
                this.document.forms[0].__EVENTTARGET.value = "";
                this.document.forms[0].__EVENTARGUMENT.value = "save3";
                document.getElementById(btnBackendSave).click();
                return false;
            }
        }

        function Save4(sMsg) {
            if (confirm(sMsg) == false) {
                return false;
            }
            this.document.forms[0].__EVENTTARGET.value = "";
            this.document.forms[0].__EVENTARGUMENT.value = "save4";
            document.getElementById(btnBackendSave).click();
            return false;
        }

        function Save5(sMsg) {
            if (confirm(sMsg) == false) {
                return false;
            }
            this.document.forms[0].__EVENTTARGET.value = "";
            this.document.forms[0].__EVENTARGUMENT.value = "save5";
            document.getElementById(btnBackendSave).click();
            return false;
        }

        //ValidateAdmin
        function Save6(sMsg, mobjAdministratorsNotFound, mobjAdministratorsInitalValue) {
            if (confirm(sMsg) == false) {
                SetActiveTab(6); //tbNoteInfo.ActiveTab = GetTabIndex("EQPROF");
                //bRateChange = Convert.ToInt32(false);
                return false;
            }
            else {
                if (mobjAdministratorsNotFound) { // Initial Value NOT Found; INVALID
                    var drpdwnlstAdmin = document.getElementById('<%= drpdwnlstAdmin.ClientID %>');
                    if (drpdwnlstAdmin.value == mobjAdministratorsInitalValue) { // Still Same
                        alert("Current 'Administrator' is not Valid, Please select a valid user");
                        SetActiveTab(0);
                        return false;
                    }
                    else {
                        return true;
                    }
                }
            }
        }

        function Save7(blnPostExtFee, nFeeAmount, bFeePostCompDate, bFeePostMaturity, isValidProp, noteType) {
            if (bFeePostCompDate != 0) {
                if (blnPostExtFee == false) {
                    alert("Extension fee cannot be calculated.  The loan is not participated or the participant interest profile is missing.");
                    //goto Continue;
                }

                if (nFeeAmount <= 0) {
                    alert("No Extension Fee Required.");
                    //goto Continue;
                }
            }

            if (bFeePostMaturity != 0) {
                //PostFee(this.NoteNumber, this.UnitNumber, cboNote[0], "NI:Renewal", , , "Renewal Fee", true);
            }

            var ddlMLoc = document.getElementById('<%= ddlMLoc.ClientID %>');
            var ddlSLoc = document.getElementById('<%= ddlSLoc.ClientID %>');
            if (ddlMLoc.selectedIndex > 0) {
                if (ddlSLoc.selectedIndex == 0) {
                    alert("If a Master LOC is selected then a Sub LOC must be selected.");
                    return false;
                }
            }
            else {
                if (ddlSLoc.selectedIndex > 0) {
                    alert("If a Sub LOC is selected then a Master LOC must be selected.");
                    return false;
                }
            }

            if (this.mblnLOCProblemOnLoad) {
                if (ddlMLoc.selectedIndex <= 0) {
                    sMsg = "While Loading this notes information, the Master/Sub LOC originally assigned could not be located" + "\n" + "\n";
                    sMsg = sMsg + "A Line of Credit has not been set for this loan and the assignemt will be removed if you save now" + "\n" + "\n";
                    sMsg = sMsg + "Press YES to continue, NO to modify.";
                    if (confirm(sMsg) == false) {
                        return false;
                    }
                }
                else {
                }
            }

            var txtDateTabQotPost = document.getElementById('<%= txtDateTabQotPost.ClientID %>');
            if (isValidProp == -1) {
                alert("There are Sub Notes attached to this Master Note which are not paid-off. You cannot input a Payoff Posted date until all Sub Notes are paid-off.");
                SetActiveTab(2);
                txtDateTabQotPost.focus();
                return false;
            }


            this.document.forms[0].__EVENTTARGET.value = "";
            this.document.forms[0].__EVENTARGUMENT.value = "save7";
            document.getElementById(btnBackendSave).click();
            return false;
            //call post fee function. Then save will be called
        }

        function LoadNonAccural() {
            var returnVal;
            var chkNonAccural = document.getElementById('<%= chkNonAccural.ClientID %>');
            var noteNo = '<%= NoteNumber %>';
            var unitNo = '<%= UnitNumber %>';
            var borrNo = '<%= BorrowerNo %>';
            returnVal = window.showModalDialog("ApplyNonAccuralNoteInfo.aspx?N=" + noteNo + "&U=" + unitNo + "&B=" + borrNo + "&CHKNONACCURAL=" + chkNonAccural.checked, "popup_window", "dialogWidth:800px;dialogHeight:280px;");
            if (returnVal == undefined) {
                //this.document.forms[0].__EVENTTARGET.value = "";
                //this.document.forms[0].__EVENTARGUMENT.value = "savefinal";
                //document.getElementById(btnBackendSave).click();
                //alert("NonAccural Failed!");
                return false;
            }
            //alert(returnVal.EffDate);
            //alert(returnVal.OldEffDate);
            this.document.forms[0].__EVENTTARGET.value = "effdate:" + returnVal.EffDate + ",oldeffdate:" + returnVal.OldEffDate;
            this.document.forms[0].__EVENTARGUMENT.value = "savefinal";
            document.getElementById(btnBackendSave).click();
            return false;
        }

        function SetActiveTab(tabNumber) {
            var tabControl = '<%= TabNoteInfo.ClientID %>';
            //var ctrl = $find(tabControl);
            //ctrl.set_activeTab(ctrl.get_tabs()[tabNumber]);
        }

        function WOpenAuditTrail(note, unit, msg) {
            window.showModalDialog('AuditReportNoteInfo.aspx?NoteNo=' + note + '&UnitNo=' + unit + '&ErrMsg=' + msg, '', 'center:yes; modal:yes; edge:Raised; resizable:no;scrollbars:no;menubar=no;status:no;dialogWidth:700px;dialogHeight:400px;');
            this.document.forms[0].__EVENTTARGET.value = "";
            this.document.forms[0].__EVENTARGUMENT.value = "auditresponse";
            document.getElementById(btnBackendSave).click();
            return false;
        }

        //Save End

        $(function() {
            $('#' + '<%# txtPrjctCity.ClientID %>').keydown(function(e) {
                if (e.shiftKey || e.ctrlKey || e.altKey) {
                    e.preventDefault();
                } else {
                    var key = e.keyCode;
                    if (!((key == 8) || (key == 32) || (key == 46) || (key >= 35 && key <= 40) || (key >= 65 && key <= 90))) {
                        e.preventDefault();
                    }
                }
            });
        });
        
    </script>

</asp:Content>


Code Behind :


using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.IO;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data;
using ISGN.Application.SessionProvider;
using ISGN.TCL.Controls.Datagrid;
using System.Collections;
using ISGN.Application.Common.Logging;
using ISGN.TCL.MODEL;
using System.Text;
using ISGN.TCL.Control.CustomGrid;
using ISGN.TCL.BL.Modules;
using ISGN.TCL.FrameWork.Base.BL;

namespace ISGN.TCL.Web.Modules.DailyProcessing
{
    public partial class NotesInfo : NoteInfoView
    {
        #region Declarations

        private NoteInfoPresenter noteInfoPresenter;
        private ISessionProvider sessionProvider = SessionProviderFactory.GetSessionProvider();
        private int iRowsPerPage = 10;
        private int iPageNumber = 1;
        //private bool mblnComRuleOverride = false;
        private bool mblnComRuleNoUpdate = false;
        private bool mblnComRuleChanged = false;
        private int mintLTOBLOC;
        private bool mblnInitLoad = false;
        private bool mblnFirstTime = false;
        string mstrExceedSUBLOC;
        public const string noteTypeBorrowerBase = "B";
        public const string noteTypeMaterNote = "M";
        public const string noteTypeSubNote = "D";
        public const string keyContEditFalse = "false";
        public const string ModifyTrue = "true";
        string Pnote = string.Empty;
        string Punit = string.Empty;
        string borrowerno = string.Empty;
        #endregion

        #region PageEvents

        protected void Page_Load(object sender, EventArgs e)
        {
            try
            {
                this.txtFincTabLoanCommit2Enabled = true;
                this.txtFincTabLoanCommit3Enabled = true;
                noteInfoPresenter = new NoteInfoPresenter(this);
                string s2 = this.NoteNumber = TCLHelper.GetData(Request.QueryString["N"]);
                string s3 = this.UnitNumber = TCLHelper.GetData(Request.QueryString["U"]);
                hdnNoteNo.Value = TCLHelper.GetData(Request.QueryString["N"]);
                hdnUnitNo.Value = TCLHelper.GetData(Request.QueryString["U"]);
                this.BorrowerNo = TCLHelper.GetData(Request.QueryString["B"]);
                sessionProvider.Set("Borrowervalues", BorrowerNo);
                sessionProvider.Set("Notevalues", NoteNumber);
                sessionProvider.Set("Unitvalues", UnitNumber);
                //this.IsNewNote = TCLHelper.ConvertToBool(Request.QueryString["IsNewNote"]);
                this.UserName = TCLHelper.GetData(sessionProvider.Get("User")).ToUpper();
                string s1 = this.NoteType = TCLHelper.GetData(Request.QueryString["NF"]);
                this.NoteMode = TCLHelper.GetData(sessionProvider.Get("gsNoteType"));
                this.IsBorrowerPortal = TCLHelper.ConvertToBool(Request.QueryString["BorrowerPortal"]);
                this.mProp_Inquiry = TCLHelper.ConvertToBool(Request.QueryString["IsInq"]);
                this.BBASE = TCLHelper.ConvertToBool(Request.QueryString["IsBase"]);
                this.Action = TCLHelper.ConvertToInt(Request.QueryString["Action"]);
                //venkatesh
                Pnote = TCLHelper.GetData(sessionProvider.Get("Notevalues"));
                Punit = TCLHelper.GetData(sessionProvider.Get("Unitvalues"));
                if (s1 == "M")
                    s1 = "Master Note - " + "&nbsp;";
                else if (s1 == "B")

                    s1 = "Borrowing Base Note - " + "&nbsp;";
                else if (s1 == "D")
                    s1 = "Sub Note - " + "&nbsp;";
                else
                    s1 = "Single Maturity Note  " + "&nbsp;" + " - " + "&nbsp;";
                lblBrwName.Text = s1 + " " + " " + s2 + "&nbsp;&nbsp; " + s3;

                sessionProvider.Set("pnote", Pnote);
                sessionProvider.Set("punit", Punit);
                //end venkatesh
                lblBorrowingBaseMsg.Visible = false;
                InitializeViewStates();
                if (TCLHelper.GetData(Request.QueryString["Inquiry"]) == "Inquiry")
                {
                    hdnInquiry.Value = "Inquiry";
                }
                if ((this.Action == 2) && (this.bRenewal != 0))
                    this.dPrevMatDate = txtDateTabMturty.Text;
                this.dPrvCompDate = txtDateTabCnsCmpl.Text;
                this.noteInfoPresenter = new NoteInfoPresenter(this);

                //if (lstbStndardArtchBrwDocTrack.Items.Count > 0)
                //    btnDoctMove.Enabled = true;
                //else
                //    btnDoctMove.Enabled = false;

                //if (lstbArtchBrwDocTrack.Items.Count > 0)
                //    btnDocRemove.Enabled = true;
                //else
                //    btnDocRemove.Enabled = false;
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Msg", "setDivWidth();", true);
                if (!IsPostBack)
                {
                    sessionProvider.Set("ModeBN", "");
                    NoteSecurity();
                    if (sessionProvider.Get("vendorName") != null)
                        sessionProvider.Clear("vendorName");
                    this.ReleaseSchNo = "1";
                    this.bLOCIntProf = false;
                    this.bLOCIntProfAdd = false;
                    this.bLOCEqtProf = false;
                    this.bLOCEqtProfAdd = false;
                    DataSet ds = this.noteInfoPresenter.LoadNoteInfo();
                    NoteinfoLoad(ds);
                    this.BindReleaseScheduleGrid(this.ListReleaseSchedule);
                    this.BindReleaseRuleGrid();
                    this.BindAttachedRuleGrid();
                    this.BindGeneral();
                    this.BindBBTerms();

                    ViewState.Add("BorrowerNo", this.BorrowerNo);
                    ViewState.Add("dPrevMatDate", this.dPrevMatDate);
                    ViewState.Add("sSubLookupIntProf", this.sSubLookupIntProf);
                    ViewState.Add("dPrvCompDate", this.dPrvCompDate);
                    ViewState.Add("nRenewalCount", this.nRenewalCount);
                    ViewState.Add("bRenewal", this.bRenewal);
                    ViewState.Add("bFeePostCompDate", this.bFeePostCompDate);
                    ViewState.Add("Action", this.Action);
                    ViewState.Add("mblnLOCProblemOnLoad", this.mblnLOCProblemOnLoad);
                    ViewState.Add("blnPostExtFee", this.blnPostExtFee);
                    ViewState.Add("nFeeAmount", this.nFeeAmount);
                    ViewState.Add("bLOCIntProfAdd", this.bLOCIntProfAdd);
                    ViewState.Add("bLOCEqtProfAdd", this.bLOCEqtProfAdd);
                    ViewState.Add("bLOCIntProf", this.bLOCIntProf);
                    ViewState.Add("bLOCEqtProf", this.bLOCEqtProf);
                    ViewState.Add("bFeePostMaturity", this.bFeePostMaturity);
                    ViewState.Add("dblMasterLookupIntProf", this.dblMasterLookupIntProf);
                    ViewState.Add("prsamt_d", this.prsamt_d);
                    ViewState.Add("pcfamt", this.pcfamt);
                    ViewState.Add("PCLAMT_D", this.PCLAMT_D);
                    ViewState.Add("PFDATE", this.PFDATE);
                    hdnBorrowerNo.Value = Convert.ToString(ViewState["BorrowerNo"]);
                    //this.noteInfoPresenter.AssignFinTabDefaultValues();
                    //this.GetGeneralNotes();
                    this.GetEquityProfileGrid();
                    this.GetIntrestProfileGrid();
                    this.BindNotePayRule();
                    string glCode = ddlGLTable.GetSelectedValue();
                    glCode = string.IsNullOrEmpty(glCode) == false ? glCode : "TCL";
                    this.noteInfoPresenter.GetTranCode(glCode);
                    BindUnitsGrid(this.noteInfoPresenter);
                    BindAuditGrid(this.noteInfoPresenter);

                    this.noteInfoPresenter.LoadDockTracking();
                    this.noteInfoPresenter.LoadDocAttach();
                    this.noteInfoPresenter.GetDated();
                    //To load Date Tab details for SubNote in future use the same function to load General tab as per ASIS
                    this.noteInfoPresenter.GetDateGeneralTab();
                    BindBorrowerAttachments();

                    // Page.ClientScript.RegisterStartupScript(upanel.GetType(), "msg", "setDivWidth();", true);
                    if (Request.QueryString["IsBase"] != null)
                    {
                        if (TCLHelper.ConvertToBool(Request.QueryString["IsBase"]) == true)
                        {
                            txtPrjctStrtAddrs.Enabled = false;
                            txtPrjctCity.Enabled = false;
                            txtPrjctCounty.Enabled = false;
                            drpdwnlstState.Enabled = false;
                            txtPrjctZipCode.Enabled = false;
                            drpdwnlstCountry.Enabled = false;
                            txtPrjctShrtLglDesc.Enabled = true;
                            txtPrjctSubDiv.Enabled = false;
                            txtPrjctPurchLoan.Enabled = true;
                            txtPrjctPrimryContrct.Enabled = false;
                            chkDualAprvl.Enabled = false;
                            txtPrjctGPS.Enabled = false;
                            txtPrjctGPS1.Enabled = false;
                            txtPrjctAccID.Enabled = true;
                            drpdwnlstAdmin.Enabled = true;
                            txtPrjctLot.Enabled = false;
                            txtPrjctBlock.Enabled = false;
                            txtPrjctSection.Enabled = false;
                            txtPrjctPhase.Enabled = false;
                            txtPrjctNetRntArea.Enabled = false;
                            btnPjrctLeasingInfo.Visible = false;
                            btnPrjctApprslInfo.Visible = false;
                            btnprjctSalescntrct.Visible = false;
                            imgbtnPrjctVendor.Enabled = false;
                            lblBorrowingBaseMsg.Visible = true;
                        }
                    }

                    if (Request.QueryString["EditMode"] != null)
                    {
                        if (Request.QueryString["EditMode"].ToString() == "False")
                        {
                            //this.noteInfoPresenter.ClearData();
                            ///VendorBudget controls-Begin
                            //imgbtnSearchVendor.Enabled = false;
                            txtVNumber.Enabled = false;
                            rbVendorRel.Enabled = false;
                            btnApply.Enabled = false;
                            egBudget.Enabled = false;
                            // btncommitalltab.Enabled = false;
                            ///VendorBudget controls-End
                        }
                    }
                    ViewState.Add("blnAUDITRPT", this.blnAUDITRPT);
                    ViewState.Add("blnAR_TAXID", this.blnAR_TAXID);
                    ViewState.Add("blnAR_LDESC", this.blnAR_LDESC);
                    ViewState.Add("blnAR_LOC", this.blnAR_LOC);
                    ViewState.Add("blnAR_LOCMAT", this.blnAR_LOCMAT);
                    ViewState.Add("blnAR_INT", this.blnAR_INT);
                    ViewState.Add("blnAR_BILLOPT", this.blnAR_BILLOPT);
                    ViewState.Add("blnAR_BUD", this.blnAR_BUD);
                    ViewState.Add("blnAR_BUDPROF", this.blnAR_BUDPROF);
                    ViewState.Add("blnAR_EQTPROF", this.blnAR_EQTPROF);
                    ViewState.Add("blnAR_LOCPARENTTOTAL", this.blnAR_LOCPARENTTOTAL);
                    ViewState.Add("blnAR_LOCTERMS", this.blnAR_LOCTERMS);

                    this.noteInfoPresenter.ComRulesSetUp();
                    this.noteInfoPresenter.ComRulesApply();
                    this.Page.DataBind();
                    this.dPrvCompDate = TCLHelper.ConvertToDateTimeFormatted(txtDateTabCnsCmpl.Text, "MM/dd/yyyy");
                    ViewState.Add("dPrvCompDate", this.dPrvCompDate);
                    this.dPrevMatDate = TCLHelper.ConvertToDateTimeFormatted(txtDateTabMturty.Text, "MM/dd/yyyy");
                    ViewState.Add("dPrevMatDate", this.dPrevMatDate);
                    this.GetGeneralNotes();
                    this.mnPrvNonAccrual = chkNonAccural.Checked;
                    ViewState.Add("mnPrvNonAccrual", this.mnPrvNonAccrual);
                    if (drpdwnlstTranscode.Items.FindByValue(this.TransValue1) != null)
                        drpdwnlstTranscode.Items.FindByValue(this.TransValue1).Selected = true;
                    if (drpdwnlstLnvlDpstEftvTrncode.Items.FindByValue(this.TransValue2) != null)
                        drpdwnlstLnvlDpstEftvTrncode.Items.FindByValue(this.TransValue2).Selected = true;
                    if (drpdwnlstLnLvlEscrwTrncode.Items.FindByValue(this.TransValue3) != null)
                        drpdwnlstLnLvlEscrwTrncode.Items.FindByValue(this.TransValue3).Selected = true;
                }
                btnDoctMove.Enabled = false;
                btnDocRemove.Enabled = false;
                imgbtnDocTracAdd.Visible = false;
                imgbtnDocTracEdit.Visible = false;

                if (sessionProvider.Get("vendorName") != null)
                    txtPrjctPrimryContrct.Text = TCLHelper.GetData(sessionProvider.Get("vendorName"));

                this.ReleaseItemSelectedValue = drpdwnlstRlsItem.GetSelectedValue();
                if (cstGrdRlsPayoffTemp.GridViewPaging.Rows.Count == 0)
                {
                    btnRlsRulesMoveRight.Enabled = false;
                }
                else
                {
                    btnRlsRulesMoveRight.Enabled = true;
                }
                if (string.Compare(this.NoteType, noteTypeBorrowerBase) == 0)
                {
                    chk203K.Enabled = false;
                    NoteTypeSecurity(false);
                    ProjectTabSecurity(false);
                    //tabPnlRelease.Visible = true;
                    //tabPnlBdgCntrl.Visible = true;
                    //tabPnlProfiles.Visible = true;
                    //tabPnlkyCnt.Visible = true;
                    TabNoteInfo.Attributes.Add("OnClientActiveTabChanged", "clientActiveTabChanged");
                    return;
                }
                // Master Note
                else if (string.Compare(this.NoteType, noteTypeMaterNote) == 0)
                {
                    NoteTypeSecurity(true);
                    ProjectTabSecurity(false);
                    NoteTypeTabSecurity(false);
                }
                // Sub Note
                else if (string.Compare(this.NoteType, noteTypeSubNote) == 0)
                {
                    NoteTypeSecurity(true);
                    ProjectTabSecurity(true);
                    NoteTypeTabSecurity(true);
                    btnprjctSalescntrct.Visible = true;
                }
                // Single Maturity Note
                else
                {
                    NoteTypeSecurity(true);
                    ProjectTabSecurity(true);
                    NoteTypeTabSecurity(true);
                }
                if (mProp_Inquiry)
                {
                    DisableAllControls();
                    btnProjectSave.Visible = false;
                }

                HideMessagePanel();
            }

            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        #endregion

        #region Security

        private void NoteTypeTabSecurity(bool status)
        {
            tabPnlRelease.Visible = status;
            tabPnlBdgCntrl.Visible = status;
            tabPnlProfiles.Visible = status;
            tabPnlkyCnt.Visible = status;
        }

        private void NoteTypeSecurity(bool status)
        {
            pnlPricipal.Visible = status;
            pnlPurchAdd.Enabled = status;
            pnlGps.Enabled = status;
            pnlPrimaryContractor.Enabled = status;
            pnlLotSec.Enabled = status;
            pnlSubDivision.Enabled = status;
            txtPrjctSubDiv.Enabled = status;
            txtPrjctLot.Enabled = status;
            txtPrjctBlock.Enabled = status;
            txtPrjctSection.Enabled = status;
            txtPrjctPhase.Enabled = status;
            tabPnlBrwBasTerms.Visible = !status;
            tabPnlBrwBasUnits.Visible = !status;
            btnPrjctApprslInfo.Visible = status;
        }

        private void ProjectTabSecurity(bool status)
        {
            btnprjctSalescntrct.Visible = status;
            btnPjrctLeasingInfo.Visible = status;
            pnlTenantSpace.Visible = status;
        }

        private void NoteSecurity()
        {
            bool chkLoanCommit;
            bool chkPrnplBalCap;
            bool chkLoanDeposit;
            bool chkEscrow;
            bool chkIntrProf;
            bool chkDocChklst;
            bool chkBdgtCtrl;
            bool chkNoteLvl;
            bool chkReleseLvl;
            bool chkAttachments;
            bool chkContInfo;
            if (sessionProvider.Get("UserSecuirtyCheck") != null)
            {
                using (DataSet ds = (DataSet)sessionProvider.Get("UserSecuirtyCheck"))
                {
                    DataRow dr = ds.Tables[0].Rows[0];
                    // Daily Processing Note Security
                    if (this.NoteMode.Equals("Property", StringComparison.OrdinalIgnoreCase))
                    {
                        // Post fees New/Edit Disable/Enable in Financial Tab
                        btnFincTabPostFee.Enabled = TCLHelper.GetData(dr["OS_OPT25"]) == "0" ? false : true;

                        //Loan Commitment in Financial Tab
                        chkLoanCommit = TCLHelper.GetData(dr["OS_OPT6"]) == "0" ? false : true;
                        // Rollback Gowtham
                        //txtFincTabLoanCommit1.Enabled = chkLoanCommit;
                        txtFincTabLoanCommit2.Enabled = chkLoanCommit;
                        txtFincTabLoanCommit3.Enabled = chkLoanCommit;
                        txtFincTabEffctDate1.Enabled = chkLoanCommit;
                        drpdwnlstTranscode.Enabled = chkLoanCommit;

                        // Commitment Rule in Financial Tab
                        chkORComRule.Enabled = TCLHelper.GetData(dr["OS_OPT64"]) == "0" ? false : true;

                        // Principal Bal.Cap in Financial Tab
                        chkPrnplBalCap = TCLHelper.GetData(dr["OS_OPT77"]) == "0" ? false : true;
                        //txtFincTabprincBal1.Enabled = chkPrnplBalCap;
                        txtFincTabprincBal2.Enabled = chkPrnplBalCap;
                        txtFincTabprincBal3.Enabled = chkPrnplBalCap;

                        // Loan level Deposit in Financial Tab
                        chkLoanDeposit = TCLHelper.GetData(dr["OS_OPT66"]) == "0" ? false : true;
                        //txtFincTabLnLvlDpst1.Enabled = chkLoanDeposit;
                        txtFincTabLnLvlDpst2.Enabled = chkLoanDeposit;
                        txtFincTabLnLvlDpst3.Enabled = chkLoanDeposit;
                        //txtFincTabEffctDate2.Enabled = chkLoanDeposit;
                        drpdwnlstLnvlDpstEftvTrncode.Enabled = chkLoanDeposit;

                        // Loan level Escrow in Financial Tab
                        chkEscrow = TCLHelper.GetData(dr["OS_OPT68"]) == "0" ? false : true;
                        //txtFincTabLnLvlEscrw1.Enabled = chkEscrow;
                        txtFincTabLnLvlEscrw2.Enabled = chkEscrow;
                        txtFincTabLnLvlEscrw3.Enabled = chkEscrow;
                        //txtFincTabEffctDate3.Enabled = chkEscrow;
                        drpdwnlstLnLvlEscrwTrncode.Enabled = chkEscrow;

                        // Maturity Date in Dates Tab
                        txtDateTabMturty.Enabled = TCLHelper.GetData(dr["OS_OPT7"]) == "0" ? false : true;
                        txtDateTabQotPayOff.Enabled = dr["Os_Opt41"].ToString() == "0" ? true : false;
                        txtDateTabQotPost.Enabled = dr["Os_Opt41"].ToString() == "0" ? true : false;

                        // Doc Tracking in Document Tab
                        ViewState["DocCheck"] = TCLHelper.GetData(dr["OS_OPT3"]) == "0" ? false : true;

                        //Budget Control Tab
                        chkBdgtCtrl = TCLHelper.GetData(dr["OS_OPT4"]) == "0" ? false : true;
                        imgbtnBdgtCntrlAdd.Visible = chkBdgtCtrl;
                        imgbtnEdit.Visible = chkBdgtCtrl;
                        ImgbtnDelete.Visible = chkBdgtCtrl;

                        // Interest Profile Tab
                        chkIntrProf = TCLHelper.GetData(dr["OS_OPT5"]) == "0" ? false : true;
                        //imgbtnIntrstPrflsAdd.Enabled = TCLHelper.GetData(dr["OS_OPT5"]) == "0" ? false : true;
                        imgbtnIntrstPrflsAdd.Visible = chkIntrProf;
                        imgbtnIntrstPrflsDel.Visible = chkIntrProf;
                        imgbtnIntrstPrflsCopy.Visible = chkIntrProf;


                        // General Tab
                        chkInDefault.Enabled = TCLHelper.GetData(dr["OS_OPT57"]) == "0" ? false : true;
                        chkNonAccural.Enabled = TCLHelper.GetData(dr["OS_OPT59"]) == "0" ? false : true;
                        chkStopFin.Enabled = TCLHelper.GetData(dr["OS_OPT20"]) == "0" ? false : true;

                        // Note Payoff Rules in Release Tab
                        chkNoteLvl = TCLHelper.GetData(dr["OS_OPT48"]) == "0" ? false : true;
                        btnPayoffMoveRight.Enabled = chkNoteLvl;
                        imgbtnNtPayoffRulsDelte.Enabled = chkNoteLvl;
                        ViewState.Add("NotePayOff", chkNoteLvl);
                        // Release Rules in Release Tab
                        ViewState["ModifyReleaseRule"] = TCLHelper.GetData(dr["OS_OPT50"]) == "0" ? false : true;
                        //chkReleseLvl = TCLHelper.GetData(dr["OS_OPT50"]) == "0" ? false : true;
                        //btnRlsRulesMoveRight.Enabled = chkReleseLvl;
                        //imgbtnRelsRulesDel.Enabled = chkReleseLvl;

                        // Attachments in Document Tab
                        ViewState["ModifyAttach"] = TCLHelper.GetData(dr["OS_OPT81"]) == "0" ? false : true;



                        // Tenant security(Leasing Info) in Project Tab
                        //have to check with Ravi
                        ViewState["LeaseInfo"] = TCLHelper.GetData(dr["OS_OPT98"]) == "0" ? false : true;

                        // Sales Contract Information in Project Tab
                        //have to check with Ravi
                        ViewState["KeyContEdit"] = TCLHelper.GetData(dr["OS_OPT100"]) == "0" ? false : true;
                        //btnKeyCntsMoveRight.Enabled = chkContInfo;
                        //imgbtnDKeyContact.Visible = chkContInfo;
                        //ViewState.Add("KeyContEdit", chkContInfo);

                        //TAB Security
                        tabPnlProject.Enabled = TCLHelper.GetData(dr["TS_OPT8"]) == "0" ? false : true;
                        tabPnlGeneral.Enabled = TCLHelper.GetData(dr["TS_OPT9"]) == "0" ? false : true;
                        tabPnlDates.Enabled = TCLHelper.GetData(dr["TS_OPT10"]) == "0" ? false : true;
                        tabPnlFinc.Enabled = TCLHelper.GetData(dr["TS_OPT11"]) == "0" ? false : true;
                        tabpnlRlsSch.Enabled = TCLHelper.GetData(dr["TS_OPT12"]) == "0" ? false : true;
                        tabPnlBdgCntrl.Enabled = TCLHelper.GetData(dr["TS_OPT13"]) == "0" ? false : true;
                        tabpnlInterestPrfl.Enabled = TCLHelper.GetData(dr["TS_OPT14"]) == "0" ? false : true;
                        tabPnlEquityPrfl.Enabled = TCLHelper.GetData(dr["TS_OPT15"]) == "0" ? false : true;
                        tabpnlDocTrack.Enabled = TCLHelper.GetData(dr["TS_OPT16"]) == "0" ? false : true;
                        tabpnlNotePayOffRules.Enabled = TCLHelper.GetData(dr["TS_OPT38"]) == "0" ? false : true;
                        tabpnlRules.Enabled = TCLHelper.GetData(dr["TS_OPT40"]) == "0" ? false : true;
                        tabPnlkyCnt.Enabled = TCLHelper.GetData(dr["TS_OPT17"]) == "0" ? false : true;
                        this.mblnCanOverrideRule = TCLHelper.GetData(dr["OS_OPT64"]) == "0" ? false : true;
                    }
                    // Pipeline Note Security
                    else if (NoteMode == "Pipeline")
                    {
                        // Post fees New/Edit Disable/Enable in Financial Tab
                        btnFincTabPostFee.Enabled = TCLHelper.GetData(dr["OS_OPT32"]) == "0" ? false : true;

                        //Loan Commitment in Financial Tab
                        chkLoanCommit = TCLHelper.GetData(dr["OS_OPT33"]) == "0" ? false : true;
                        // Rollback Gowtham
                        //txtFincTabLoanCommit1.Enabled = chkLoanCommit;
                        txtFincTabLoanCommit2.Enabled = chkLoanCommit;
                        txtFincTabLoanCommit3.Enabled = chkLoanCommit;
                        txtFincTabEffctDate1.Enabled = chkLoanCommit;
                        drpdwnlstTranscode.Enabled = chkLoanCommit;

                        // Commitment Rule in Financial Tab
                        chkORComRule.Enabled = TCLHelper.GetData(dr["OS_OPT65"]) == "0" ? false : true;

                        // Principal Bal.Cap in Financial Tab
                        chkPrnplBalCap = TCLHelper.GetData(dr["OS_OPT76"]) == "0" ? false : true;
                        //txtFincTabprincBal1.Enabled = chkPrnplBalCap;
                        txtFincTabprincBal2.Enabled = chkPrnplBalCap;
                        txtFincTabprincBal3.Enabled = chkPrnplBalCap;

                        // Loan level Deposit in Financial Tab
                        chkLoanDeposit = TCLHelper.GetData(dr["OS_OPT67"]) == "0" ? false : true;
                        //txtFincTabLnLvlDpst1.Enabled = chkLoanDeposit;
                        txtFincTabLnLvlDpst2.Enabled = chkLoanDeposit;
                        txtFincTabLnLvlDpst3.Enabled = chkLoanDeposit;
                        txtFincTabEffctDate2.Enabled = chkLoanDeposit;
                        drpdwnlstLnvlDpstEftvTrncode.Enabled = chkLoanDeposit;

                        // Loan level Escrow in Financial Tab
                        chkEscrow = TCLHelper.GetData(dr["OS_OPT69"]) == "0" ? false : true;
                        //txtFincTabLnLvlEscrw1.Enabled = chkEscrow;
                        txtFincTabLnLvlEscrw2.Enabled = chkEscrow;
                        txtFincTabLnLvlEscrw3.Enabled = chkEscrow;
                        txtFincTabEffctDate3.Enabled = chkEscrow;
                        drpdwnlstLnLvlEscrwTrncode.Enabled = chkEscrow;

                        // Maturity Date in Dates Tab
                        txtDateTabMturty.Enabled = TCLHelper.GetData(dr["OS_OPT34"]) == "0" ? false : true;
                        txtDateTabQotPayOff.Enabled = TCLHelper.GetData(dr["Os_Opt41"]) == "0" ? true : false;
                        txtDateTabQotPost.Enabled = TCLHelper.GetData(dr["Os_Opt41"]) == "0" ? true : false;

                        // Doc Tracking in Document Tab
                        ViewState["DocCheck"] = TCLHelper.GetData(dr["OS_OPT35"]) == "0" ? false : true;

                        //Budget Control Tab
                        chkBdgtCtrl = TCLHelper.GetData(dr["OS_OPT36"]) == "0" ? false : true;
                        imgbtnBdgtCntrlAdd.Visible = chkBdgtCtrl;
                        imgbtnEdit.Visible = chkBdgtCtrl;
                        ImgbtnDelete.Visible = chkBdgtCtrl;

                        // Interest Profile Tab                        
                        chkIntrProf = TCLHelper.GetData(dr["OS_OPT37"]) == "0" ? false : true;
                        imgbtnIntrstPrflsAdd.Visible = chkIntrProf;
                        imgbtnIntrstPrflsDel.Visible = chkIntrProf;
                        imgbtnIntrstPrflsCopy.Visible = chkIntrProf;

                        // General Tab
                        chkInDefault.Enabled = TCLHelper.GetData(dr["OS_OPT56"]) == "0" ? false : true;
                        chkNonAccural.Enabled = TCLHelper.GetData(dr["OS_OPT58"]) == "0" ? false : true;
                        chkStopFin.Enabled = TCLHelper.GetData(dr["OS_OPT38"]) == "0" ? false : true;

                        // Note Payoff Rules in Release Tab
                        chkNoteLvl = TCLHelper.GetData(dr["OS_OPT47"]) == "0" ? false : true;
                        btnPayoffMoveRight.Enabled = chkNoteLvl;
                        imgbtnNtPayoffRulsDelte.Enabled = chkNoteLvl;
                        ViewState.Add("NotePayOff", chkNoteLvl);
                        // Release Rules in Release Tab
                        ViewState["ModifyReleaseRule"] = TCLHelper.GetData(dr["OS_OPT49"]) == "0" ? false : true;



                        // Attachments in Document Tab
                        ViewState["ModifyAttach"] = TCLHelper.GetData(dr["OS_OPT80"]) == "0" ? false : true;
                        //chkAttachments = dr["OS_OPT80"].ToString() == "0" ? false : true;



                        // Tenant security(Leasing Info) in Project Tab
                        //have to check with Ravi
                        ViewState["LeaseInfo"] = TCLHelper.GetData(dr["OS_OPT97"]) == "0" ? false : true;

                        // Sales Contract Information in Project Tab
                        //have to check with Ravi
                        ViewState["KeyContEdit"] = TCLHelper.GetData(dr["OS_OPT99"]) == "0" ? false : true;
                        //btnKeyCntsMoveRight.Enabled = chkContInfo;
                        //imgbtnDKeyContact.Visible = chkContInfo;
                        //ViewState.Add("KeyContEdit", chkContInfo);

                        //TAB Security
                        tabPnlProject.Enabled = TCLHelper.GetData(dr["TS_OPT25"]) == "0" ? false : true;         // Project
                        tabPnlGeneral.Enabled = TCLHelper.GetData(dr["TS_OPT26"]) == "0" ? false : true;         // General
                        tabPnlDates.Enabled = TCLHelper.GetData(dr["TS_OPT27"]) == "0" ? false : true;          // Dates
                        tabPnlFinc.Enabled = TCLHelper.GetData(dr["TS_OPT28"]) == "0" ? false : true;           // Financial
                        tabpnlRlsSch.Enabled = TCLHelper.GetData(dr["TS_OPT29"]) == "0" ? false : true;         // Release Schedule
                        tabPnlBdgCntrl.Enabled = TCLHelper.GetData(dr["TS_OPT30"]) == "0" ? false : true;       // Budget Control
                        tabpnlInterestPrfl.Enabled = TCLHelper.GetData(dr["TS_OPT31"]) == "0" ? false : true;   // Interest Profile
                        tabPnlEquityPrfl.Enabled = TCLHelper.GetData(dr["TS_OPT32"]) == "0" ? false : true;     // Equity Profile
                        tabpnlDocTrack.Enabled = TCLHelper.GetData(dr["TS_OPT33"]) == "0" ? false : true;       // Doc Tracking
                        tabpnlNotePayOffRules.Enabled = TCLHelper.GetData(dr["TS_OPT37"]) == "0" ? false : true;// Note Payoff Rules    
                        tabpnlRules.Enabled = TCLHelper.GetData(dr["TS_OPT39"]) == "0" ? false : true;          // Release Rules
                        tabPnlkyCnt.Enabled = TCLHelper.GetData(dr["TS_OPT34"]) == "0" ? false : true;          // Key Content
                        this.mblnCanOverrideRule = TCLHelper.GetData(dr["OS_OPT65"]) == "0" ? false : true;
                    }
                    if (ds.IsTableExists(1))
                    {
                        this.blnAUDITRPT = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AUDITRPT"].ToString());
                        this.blnAR_TAXID = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_TAXID"].ToString());
                        this.blnAR_LDESC = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_LDESC"].ToString());
                        this.blnAR_LOC = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_LOC"].ToString());
                        this.blnAR_LOCMAT = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_LOCMAT"].ToString());
                        this.blnAR_INT = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_INT"].ToString());
                        this.blnAR_BILLOPT = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_BILLOPT"].ToString());
                        this.blnAR_BUD = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_BUD"].ToString());
                        this.blnAR_BUDPROF = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_BUDPROF"].ToString());
                        this.blnAR_EQTPROF = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_EQTPROF"].ToString());
                        this.blnAR_LOCPARENTTOTAL = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_LOCPARENTTOTAL"].ToString());
                        this.blnAR_LOCTERMS = TCLHelper.ConvertToTCLBool(ds.Tables[1].Rows[0]["AR_LOC"].ToString());
                    }
                }
            }
        }

        private void DisableAllControls()
        {
            foreach (AjaxControlToolkit.TabPanel tabPanel in TabNoteInfo.Tabs)
            {
                foreach (System.Web.UI.Control control in tabPanel.Controls)
                {
                    Disable(control);
                }
            }
        }

        private void Disable(System.Web.UI.Control control)
        {
            if (control.Controls.Count > 0)
            {
                foreach (System.Web.UI.Control ctrl in control.Controls)
                {
                    Disable(ctrl);
                }
            }
            else
            {
                if (control.GetType().GetProperty("Enabled") != null)
                {
                    control.GetType().GetProperty("Enabled").SetValue(control, false, null);
                }
            }
        }

        #endregion

        #region Control Events

        protected void ImgbtnIntrstPrflsAdd_Click(object sender, EventArgs e)
        {
            string method = "ADD";
            string source = "INOTE";

            //int intAmort = chkAmortizeLoan.Checked == true ? 1 : 0;
            int intDefault = chkInDefault.Checked == true ? 1 : 0;


            string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "', '" + intDefault + "')";
            InvokeJavascriptFunction(script);
        }

        protected void ImgbtnIntrstPrflsCopy_Click(object sender, EventArgs e)
        {
            string method = "COPY";
            string source = "INOTE";
            string effectiveDate = string.Empty;
            int selectedIndex = 0;
            if (IsGridrowSelected(CGIntrestProfile, ref selectedIndex))
            {
                effectiveDate = hdnIPEffDate.Value;
                sessionProvider.Set("IEFFDATE", effectiveDate);
            }

            string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "')";
            InvokeJavascriptFunction(script);
        }

        protected void ImgbtEqtyPrflsAdd_Click(object sender, EventArgs e)
        {
            string method = "ADD";
            string source = "EQTYPROF";
            string equityType = string.Empty;
            string budgetID = string.Empty;

            string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "', '" + equityType + "', '" + budgetID + "')";
            InvokeJavascriptFunction(script);
        }

        protected void imgbtEqtyPrflsCopy_Click(object sender, EventArgs e)
        {
            string method = "COPY";
            string source = "EQTYPROF";
            string effectiveDate = string.Empty;
            string equityType = string.Empty;
            string budgetID = string.Empty;
            int selectedIndex = 0;
            if (IsGridrowSelected(CGEquityProfile, ref selectedIndex))
            {
                sessionProvider.Set("IEFFDATE", hdnEPEffDate.Value);
                equityType = CGEquityProfile.GridViewPaging.Rows[selectedIndex].Cells[4].Text;
                budgetID = CGEquityProfile.GridViewPaging.Rows[selectedIndex].Cells[3].Text;
            }

            string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "', '" + equityType + "', '" + budgetID + "')";
            InvokeJavascriptFunction(script);
        }

        protected void gvAttachments_GridPaging(object sender, EventArgs e)
        {
            iPageNumber = gvAttachments.PageNumber;
            iRowsPerPage = gvAttachments.RowsPerPage;
            BindBorrowerAttachments();
        }

        protected void CGIntrestProfile_GridRowEditing(object sender, EventArgs e)
        {
            try
            {
                string method = "MOD";
                string source = "INOTE";
                string effectiveDate = string.Empty;
                GridViewRow gvr = ((TCL.Control.CustomGrid.ExtendGrid)(sender)).SelectedRow;
                effectiveDate = ((LinkButton)gvr.Cells[2].Controls[0]).Text;
                sessionProvider.Set("IEFFDATE", effectiveDate);                
                //int intAmort = chkAmortizeLoan.Checked == true ? 1 : 0;
                int intDefault = chkInDefault.Checked == true ? 1 : 0;
                string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "', '" + intDefault + "'" + "," + "0" + ")";
                InvokeJavascriptFunction(script);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
                throw;
            }
        }

        protected void CGEquityProfile_GridRowEditing(object sender, EventArgs e)
        {
            try
            {
                string method = "MOD";
                string source = "EQTYPROF";
                string effectiveDate = string.Empty;
                string equityType = string.Empty;
                string budgetID = string.Empty;

                GridViewRow gvr = ((TCL.Control.CustomGrid.ExtendGrid)(sender)).SelectedRow;
                effectiveDate = ((LinkButton)gvr.Cells[5].Controls[0]).Text;
                sessionProvider.Set("IEFFDATE", effectiveDate);
                equityType = gvr.Cells[4].Text;
                budgetID = gvr.Cells[3].Text;

                string script = "LoadIPEQWindow('" + this.NoteNumber + "', '" + this.UnitNumber + "', '" + method + "', '" + source + "', '" + this.BorrowerNo + "', '" + this.LCSeq + "', '" + this.dblLOCMID + "', '" + this.mProp_Inquiry + "', '" + equityType + "', '" + budgetID + "')";
                InvokeJavascriptFunction(script);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
                throw;
            }
        }

        protected void btnTabIntrstprflTranches_Click(object sender, EventArgs e)
        {
            Response.Redirect("~/Modules/DailyProcessing/TrancheTieredPricing.aspx?Mode=Note&Pnoteno=" + this.NoteNumber + "&punit=" + this.UnitNumber + "");
        }

        protected void btnHideKeyContects_Click(object sender, EventArgs e)
        {
            txtFindContact.Text = string.Empty;
            BindKeyContacts();
        }
        #endregion

        #region BorrowingBase Units Shalin
        protected void btnRedirectUnits_Click(object sender, EventArgs e)
        {
            noteInfoPresenter = new NoteInfoPresenter(this);
            BindUnitsGrid(noteInfoPresenter);
            BindAuditGrid(noteInfoPresenter);
        }

        protected void btnRedirectTerms_Click(object sender, EventArgs e)
        {
            BindBBTerms();
        }

        private void BindUnitsGrid(NoteInfoPresenter objPresenter)
        {
            string strFilter = string.Empty;
            //string Pnote = TCLHelper.GetData(sessionProvider.Get("Notevalues"));
            //string Punit = TCLHelper.GetData(sessionProvider.Get("Unitvalues"));
            //sessionProvider.Set("pnote", Pnote);
            //sessionProvider.Set("punit", Punit);
            if (sessionProvider.Get("BBUnitFilter") != null)
            {
                strFilter = TCLHelper.GetData(sessionProvider.Get("BBUnitFilter"));
            }
            using (DataSet ds = objPresenter.GetBBCollateralByNoteUnit(
                        TCLHelper.GetData(sessionProvider.Get("gsNoteType")),
                    Pnote, Punit, string.Empty, false, strFilter))
            {
                GVUnitTerms.Visible = true;
                GVUnitTerms.GridAllowPaging = false;

                GVUnitTerms.DataKeyNames = new string[] { "P_PNOTENO", "P_PUNIT" };
                GVUnitTerms.ShowColumns = new int[] { 0, 1, 2, 3, 4, 5, 6, 7 };
                GVUnitTerms.GridShowFooter = true;
                GVUnitTerms.GridWidth = Unit.Percentage(100);
                GVUnitTerms.DataSource = ds;
                GVUnitTerms.BindGrid();
            }
        }

        private void BindAuditGrid(NoteInfoPresenter objPresenter)
        {
            string Pnote = TCLHelper.GetData(sessionProvider.Get("Notevalues"));
            string Punit = TCLHelper.GetData(sessionProvider.Get("Unitvalues"));

            using (DataSet ds = objPresenter.GetBBAuditLogRecords(
                    Pnote, Punit, 0))
            {
                GVUnitAuditLog.Visible = true;
                GVUnitAuditLog.GridAllowPaging = false;
                GVUnitAuditLog.DataKeyNames = new string[] { "PNOTENO", "PUNIT" };
                GVUnitAuditLog.ShowColumns = new int[] { 1, 3, 4, 5 };
                GVUnitAuditLog.GridShowFooter = true;
                GVUnitAuditLog.AllowLinks = new int[] { 1 };
                GVUnitAuditLog.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                GVUnitAuditLog.GridWidth = Unit.Percentage(100);
                GVUnitAuditLog.DataSource = ds;
                GVUnitAuditLog.BindGrid();
            }
        }

        //protected void btnBrwBaseFilter_Click(object sender, EventArgs e)
        //{
        //    Response.Redirect("BBUnitFilter.aspx");
        //}

        //protected void btnBrwBaseMangUnits_Click(object sender, EventArgs e)
        //{
        //    Response.Redirect("Borroweringbaseunit.aspx");
        //}

        //protected void btnBrwBstabLogUnit1_Click(object sender, EventArgs e)
        //{
        //    string redirectUrl = string.Empty;
        //    if (txtAuditLog1.Text != string.Empty)
        //        redirectUrl = "BBUnitAuditLog.aspx?Category=3&AuditDate=" + txtAuditLog1.Text.Replace("/", "-");
        //    else
        //        redirectUrl = "BBUnitAuditLog.aspx?Category=3";
        //    Response.Redirect(redirectUrl);
        //}

        //protected void btnBrwBstabLogUnit2_Click(object sender, EventArgs e)
        //{
        //    string redirectUrl = string.Empty;
        //    if (txtAuditLog1.Text != string.Empty)
        //        redirectUrl = "BBUnitAuditLog.aspx?Category=1&AuditDate=" + txtAuditLog1.Text.Replace("/", "-");
        //    else
        //        redirectUrl = "BBUnitAuditLog.aspx?Category=1";
        //    Response.Redirect(redirectUrl);
        //}

        //protected void ImgAuditAdd_Click(object sender, ImageClickEventArgs e)
        //{
        //    Response.Redirect("BBUnitAuditLog.aspx?Category=2");
        //}

        protected void ImgAuditDelete_Click(object sender, ImageClickEventArgs e)
        {
            noteInfoPresenter = new NoteInfoPresenter(this);
            bool success = false;
            string msg = string.Empty;
            if (ViewState["AuditID"] == null)
            {
                noteInfoPresenter.ShowMessageBox("Please select a record to delete");
                return;
            }
            success = noteInfoPresenter.DeleteAuditRecord(TCLHelper.ConvertToDouble(ViewState["AuditID"]));
            BindAuditGrid(noteInfoPresenter);

            lblErrorFail.Text = "Deleted Successfully";
        }

        protected void GVUnitAuditLog_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            GridViewRow gvRow = GVUnitAuditLog.SelectedRow;
            string Recid = gvRow.Cells[1].Text;
            ImageButton SelectUnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
            if (SelectUnSelect.AlternateText == "1")
            {
                hdnAuditDelete.Value = "1";
                ViewState["AuditID"] = TCLHelper.GetData(gvRow.Cells[1].Text);
            }
            else
            {
                hdnAuditDelete.Value = "0";
                ViewState["AuditID"] = null;
            }
        }

        protected void GVUnitAuditLog_GridRowEditing(object sender, EventArgs e)
        {
            GridViewRow gvRow = GVUnitAuditLog.SelectedRow;
            string Recid = gvRow.Cells[1].Text;
            sessionProvider.Set("GVUnitAuditLog", true);
            ScriptManager.RegisterStartupScript(Page, Page.GetType(),
                        "Script", "WOpen('bbu','" + Recid + "');", true);
        }
        #endregion

        #region Shanki(Project,Release,Rules)

        private void BindAttachedRuleGrid()
        {
            using (DataSet dsAttchRg = this.noteInfoPresenter.LoadAttachedReleaseRule())
            {
                if (dsAttchRg.IsValidDataColumn())
                {
                    cstGrdRlsPayoffAtchmnt.GridRowStyleCSS = "normalrow";
                    cstGrdRlsPayoffAtchmnt.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    cstGrdRlsPayoffAtchmnt.GridAlternatingRowCSS = "altrow";
                    //cstGrdRlsPayoffAtchmnt.GridClientID = "cstGrdRlsPayoffAtchmnt";
                    cstGrdRlsPayoffAtchmnt.GridAllowPaging = false;
                    cstGrdRlsPayoffAtchmnt.GridWidth = Unit.Percentage(100);
                    cstGrdRlsPayoffAtchmnt.ShowColumns = new int[] { 0, 1, 2 };
                    cstGrdRlsPayoffAtchmnt.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Multiple;
                    cstGrdRlsPayoffAtchmnt.DataSource = dsAttchRg;
                    cstGrdRlsPayoffAtchmnt.BindGrid();
                }
            }
        }

        private void BindReleaseRuleGrid()
        {
            using (DataSet ds = this.noteInfoPresenter.LoadReleaseRules())
            {
                if (ds.IsValidDataColumn())
                {
                    cstGrdRlsPayoffTemp.GridRowStyleCSS = "normalrow";
                    cstGrdRlsPayoffTemp.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    cstGrdRlsPayoffTemp.GridAlternatingRowCSS = "altrow";
                    //cstGrdRlsPayoffTemp.GridClientID = "cstGrdRlsPayoffTemp";
                    cstGrdRlsPayoffTemp.GridAllowPaging = false;
                    cstGrdRlsPayoffTemp.GridWidth = Unit.Percentage(100);
                    cstGrdRlsPayoffTemp.ShowColumns = new int[] { 0, 1, 2 };
                    cstGrdRlsPayoffTemp.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Multiple;
                    cstGrdRlsPayoffTemp.DataSource = ds;
                    cstGrdRlsPayoffTemp.BindGrid();
                }
            }
        }

        private void BindReleaseScheduleGrid(List<ReleaseScheduleGrid> lstReleaseSchedule)
        {
            imgbtnRelsSchDel.Visible = false;
            imgbtnRelsSchEdit.Visible = false;
            if (lstReleaseSchedule != null && lstReleaseSchedule.Count > 0)
            {
                imgbtnRelsSchDel.Visible = true;
                imgbtnRelsSchEdit.Visible = true;
                hdnItemID.Value = string.Empty;
                grdRlsSch.GridRowStyleCSS = "normalrow";
                grdRlsSch.GridHeaderRowCSS = "pl10 pr10 gridheader";
                grdRlsSch.GridAlternatingRowCSS = "altrow";
                //grdRlsSch.GridClientID = "grdRlsSch";
                grdRlsSch.GridAllowPaging = false;
                grdRlsSch.AllowLinks = new int[] { 0 };
                grdRlsSch.GridShowFooter = true;
                grdRlsSch.GridWidth = Unit.Percentage(100);
                grdRlsSch.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                grdRlsSch.DataKeyNames = new string[] { "Item" };
                grdRlsSch.ShowColumns = new int[] { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11 };
                grdRlsSch.BindGrid<ReleaseScheduleGrid>(lstReleaseSchedule);
            }
            else
            {
                lstReleaseSchedule = new List<ReleaseScheduleGrid>();
                hdnItemID.Value = string.Empty;
                grdRlsSch.GridRowStyleCSS = "normalrow";
                grdRlsSch.GridHeaderRowCSS = "pl10 pr10 gridheader";
                grdRlsSch.GridAlternatingRowCSS = "altrow";
                //grdRlsSch.GridClientID = "grdRlsSch";
                grdRlsSch.GridAllowPaging = false;
                grdRlsSch.AllowLinks = new int[] { 0 };
                grdRlsSch.GridShowFooter = true;
                grdRlsSch.GridWidth = Unit.Percentage(100);
                grdRlsSch.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                grdRlsSch.DataKeyNames = new string[] { "Item" };
                grdRlsSch.ShowColumns = new int[] { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11 };
                grdRlsSch.DataSource = null;
                //grdRlsSch.BindGrid<ReleaseScheduleGrid>(lstReleaseSchedule);
                grdRlsSch.BindGrid();
                grdRlsSch.GridViewPaging.DataSource = null;
                grdRlsSch.GridViewPaging.DataBind();
            }
        }

        private List<ReleaseScheduleGrid> ConvertDataSetToList(ref bool isSelected, ref int selectedIndex)
        {
            var categoryList = new List<ReleaseScheduleGrid>();
            int index = 0;
            foreach (GridViewRow row in grdRlsSch.GridViewPaging.Rows)
            {
                ReleaseScheduleGrid category = new ReleaseScheduleGrid()
                {
                    Item = TCLHelper.RemoveHtmlWhiteSpace(((System.Web.UI.WebControls.LinkButton)(row.Cells[1].Controls[0])).Text),
                    Description = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[2].Text),
                    MinimumAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[3].Text),
                    ReleaseAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[4].Text),
                    LastReleaseDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[5].Text),
                    Status = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[6].Text),
                    ReleaseDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[7].Text),
                    AppraisedAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[8].Text),
                    AppraisalDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[9].Text),
                    Type = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[10].Text),
                    DiscountedAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[11].Text),
                    QuoteDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[12].Text),
                    PayDownFlag = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[13].Text),
                    rssamt = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[14].Text),
                    rsspsqft = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[15].Text),
                    rsssqft = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[16].Text),
                    rsvpsqft = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[17].Text),
                    rsvsqft = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[18].Text),
                };

                ImageButton selectButton = (ImageButton)row.FindControl("imgRowSelect");
                if (selectButton.AlternateText == "1")
                {
                    selectedIndex = index;
                    isSelected = true;
                }

                categoryList.Add(category);
                index += 1;
            }

            return categoryList;
        }

        protected void imgbtnRelsRulesDel_Click(object sender, ImageClickEventArgs e)
        {
            bool bFlag = false;
            foreach (GridViewRow gridViewRow in cstGrdRlsPayoffAtchmnt.GridViewPaging.Rows)
            {
                CheckBox chkRowSelect = (gridViewRow.Cells[0].FindControl("chkMultipleSelect") as CheckBox);
                if (chkRowSelect.Checked == true)
                {
                    bFlag = true;
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "DeleteNoteReleasePayOff('Are you sure you want to remove selected Payoff Rule(s)?');", true);
                    return;
                }
            }
            if (!bFlag)
            {
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alert", "alert('No Rule(s) selected to remove.');", true);
                return;
            }

            //RemoveRuleItem strRuleID, "", "PAYOFFRULESRELEASE", goNoteInfo.NoteNum, goNoteInfo.UnitNum, strRsItem$
        }

        protected void btnRelsRulesDelete_Click(object sender, EventArgs e)
        {
            foreach (GridViewRow gridViewRow in cstGrdRlsPayoffAtchmnt.GridViewPaging.Rows)
            {
                CheckBox chkChecked = (CheckBox)gridViewRow.FindControl("chkMultipleSelect");
                if (chkChecked.Checked)
                {
                    string ruleId = TCLHelper.RemoveHtmlWhiteSpace(gridViewRow.Cells[2].Text);
                    string rsitem = drpdwnlstRlsItem.GetSelectedValue();
                    string errorCode = string.Empty;
                    this.noteInfoPresenter.RemoveRuleItem(ruleId, string.Empty, "PAYOFFRULESRELEASE", this.NoteNumber, this.UnitNumber, rsitem, out errorCode);
                }
            }
            BindAttachedRuleGrid();
            BindReleaseRuleGrid();
        }

        protected void imgbtnRelsSchAdd_Click(object sender, ImageClickEventArgs e)
        {
            List<ReleaseScheduleGrid> listReleaseSch = null;
            if (grdRlsSch.GridViewPaging.Rows.Count == 0)
            {
                listReleaseSch = new List<ReleaseScheduleGrid>();
                int totalcount = TCLHelper.ConvertToInt(txtRlsSchTabNum.Text);
                for (int i = 0; i < totalcount; i++)
                {
                    ReleaseScheduleGrid releaseScheduleGrid = new ReleaseScheduleGrid();
                    if (i == 0)
                    {
                        releaseScheduleGrid.Item = "00001";
                        listReleaseSch.Add(releaseScheduleGrid);
                    }
                    else
                    {
                        releaseScheduleGrid.Item = listReleaseSch.Max(a => TCLHelper.ConvertToInt(a.Item) + 1).ToString("00000");
                        listReleaseSch.Add(releaseScheduleGrid);
                    }

                    this.noteInfoPresenter.InsertReleaseSchedule(releaseScheduleGrid);
                }
            }
            else
            {
                bool isSelected = false;
                int selectedIndex = -1;
                listReleaseSch = this.ConvertDataSetToList(ref isSelected, ref selectedIndex);
                if (selectedIndex > -1 && isSelected == true)
                {
                    for (int i = 0; i < TCLHelper.ConvertToInt(txtRlsSchTabNum.Text); i++)
                    {
                        string rlsItem = listReleaseSch.Max(a => TCLHelper.ConvertToInt(a.Item) + 1).ToString("00000");
                        ReleaseScheduleGrid relsSchGrid = new ReleaseScheduleGrid()
                        {
                            Item = listReleaseSch.Max(a => TCLHelper.ConvertToInt(a.Item) + 1).ToString("00000"),
                            Description = listReleaseSch[selectedIndex].Description,
                            MinimumAmount = listReleaseSch[selectedIndex].MinimumAmount,
                            ReleaseAmount = listReleaseSch[selectedIndex].ReleaseAmount,
                            LastReleaseDate = listReleaseSch[selectedIndex].LastReleaseDate,
                            Status = listReleaseSch[selectedIndex].Status,
                            ReleaseDate = listReleaseSch[selectedIndex].ReleaseDate,
                            AppraisedAmount = listReleaseSch[selectedIndex].AppraisedAmount,
                            AppraisalDate = listReleaseSch[selectedIndex].AppraisalDate,
                            Type = listReleaseSch[selectedIndex].Type,
                            DiscountedAmount = listReleaseSch[selectedIndex].DiscountedAmount,
                            QuoteDate = listReleaseSch[selectedIndex].QuoteDate,
                            PayDownFlag = listReleaseSch[selectedIndex].PayDownFlag,
                            rssamt = listReleaseSch[selectedIndex].rssamt,
                            rsspsqft = listReleaseSch[selectedIndex].rsspsqft,
                            rsssqft = listReleaseSch[selectedIndex].rsssqft,
                            rsvpsqft = listReleaseSch[selectedIndex].rsvpsqft,
                            rsvsqft = listReleaseSch[selectedIndex].rsvsqft,
                        };
                        listReleaseSch.Add(relsSchGrid);
                        this.noteInfoPresenter.InsertReleaseSchedule(relsSchGrid);
                    }
                }
                else
                {
                    List<ReleaseScheduleGrid> listReleaseSchInsert = new List<ReleaseScheduleGrid>();
                    for (int i = 0; i < TCLHelper.ConvertToInt(txtRlsSchTabNum.Text); i++)
                    {
                        if (listReleaseSchInsert.Count == 0)
                        {
                            listReleaseSchInsert.Add(new ReleaseScheduleGrid() { Item = listReleaseSch.Max(a => TCLHelper.ConvertToInt(a.Item) + 1).ToString("00000") });
                        }
                        else
                        {
                            listReleaseSchInsert.Add(new ReleaseScheduleGrid() { Item = listReleaseSchInsert.Max(a => TCLHelper.ConvertToInt(a.Item) + 1).ToString("00000") });
                        }
                        this.noteInfoPresenter.InsertReleaseSchedule(listReleaseSchInsert[i]);
                    }
                    listReleaseSch = listReleaseSch.Concat(listReleaseSchInsert).ToList();
                }
                //grdRlsSch.DataSource = listReleaseSch;
                //grdRlsSch.BindGrid<ReleaseScheduleGrid>(listReleaseSch);                
            }

            BindReleaseScheduleGrid(listReleaseSch);


            if (grdRlsSch.GridViewPaging.Rows.Count > 0)
            {
                drpdwnlstRlsItem.Items.Clear();
                this.noteInfoPresenter.LoadReleaseItems();
                drpdwnlstRlsItem.DataBind();
            }
        }
        protected void btnCancelRelschUpdate_Click(object sender, EventArgs e)
        {
            mdlPopupRelschUpdate.Hide();
        }

        protected void imgbtnRelsSchEdit_Click(object sender, ImageClickEventArgs e)
        {
            // mdlPopupRelSchdle.Show();
            ScriptManager.RegisterStartupScript(Page, this.GetType(), "Open", "javascript:Open();", true);

        }

        public bool IsGridrowSelected(ExtendGrid gridName, ref int selectedIndex)
        {
            int index = 0;
            foreach (GridViewRow gvRow in gridName.GridViewPaging.Rows)
            {
                ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                if (selectButton.AlternateText == "1")
                {
                    LinkButton lnkButton = (LinkButton)gvRow.FindControl("lnk0");
                    selectedIndex = index;
                    return true;
                }

                index += 1;
            }

            return false;
        }

        protected void imgbtnRelsSchDel_Click(object sender, ImageClickEventArgs e)
        {
            //if (TCLHelper.ConvertToInt(adoRelsch!RSAAMT)==0) { 
            //RemoveRuleItem("", TCLHelper.GetData(adoSetupModTable("PBNUMBER")), "PAYOFFRULESRELEASE", goNoteInfo.NoteNum, goNoteInfo.UnitNum, pubFmtRelColItem(TCLHelper.GetData(adoRelsch("RSITEM"))));
            //adoRelsch.Requery(); 
            //fplstRelsch.DataSource = adoRelsch; 
            //if (adoRelsch.RecordCount==0) { 
            //lblHiddenRel.Text = Convert.ToString(O);
            // ---------------------------------------------------------------------------Ravi Shankar Sundaram
            //1:42 PM
            //} else { 
            //adoRelsch.MoveLast(); 
            //lblHiddenRel.Text = pubFmtRelColItem(TCLHelper.GetData((adoRelsch!RSITEM))); 
            //} 
            //} else { 
            //MessageBox.Show("Cannot delete release schedule"+gsCR_LF+TCLHelper.GetData(adoRelsch!RSDESC)+gsCR_LF+"Release Amount: "+(TCLHelper.ConvertToInt(adoRelsch!RSAAMT)).ToString("Currency"),"Delete Not Allowed", vbCritical+vbOKOnly, vbCritical+vbOKOnly); 
            //} 
            //SetButtons(); // Set cmd(2-5) 
            //if (fplstRelsch.Enabled) fplstRelsch.Focus(); 
            //} 
            int selectedIndex = 0;
            bool isSelected = IsGridrowSelected(grdRlsSch, ref selectedIndex);
            if (isSelected)
            {
                this.noteInfoPresenter.DeleteRelease(hdnItemID.Value);
                string errorCode = string.Empty;
                this.noteInfoPresenter.RemoveRuleItem(string.Empty, this.BorrowerNo, "PAYOFFRULESRELEASE", this.NoteNumber, this.UnitNumber, "", out errorCode);

                var categoryList = new List<ReleaseScheduleGrid>();
                foreach (GridViewRow row in grdRlsSch.GridViewPaging.Rows)
                {
                    ReleaseScheduleGrid category = new ReleaseScheduleGrid()
                    {
                        Item = TCLHelper.RemoveHtmlWhiteSpace(((System.Web.UI.WebControls.LinkButton)(row.Cells[1].Controls[0])).Text),
                        Description = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[2].Text),
                        MinimumAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[3].Text),
                        ReleaseAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[4].Text),
                        LastReleaseDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[5].Text),
                        Status = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[6].Text),
                        ReleaseDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[7].Text),
                        AppraisedAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[8].Text),
                        AppraisalDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[9].Text),
                        Type = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[10].Text),
                        DiscountedAmount = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[11].Text),
                        QuoteDate = TCLHelper.RemoveHtmlWhiteSpace(row.Cells[12].Text)
                    };
                    if (hdnItemID.Value != TCLHelper.RemoveHtmlWhiteSpace(((System.Web.UI.WebControls.LinkButton)(row.Cells[1].Controls[0])).Text))
                    {
                        categoryList.Add(category);
                    }
                }
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Selected Release schedule deleted Successfully.');", true);
                BindReleaseScheduleGrid(categoryList);
            }
            else
            {
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Must select a Release schedule before delete.');", true);
            }
        }

        protected void grdRlsSch_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            GridViewRow gvRow = grdRlsSch.SelectedRow;
            ImageButton SelectUnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
            if (SelectUnSelect.AlternateText == "1")
            {
                hdnItemID.Value = TCLHelper.RemoveHtmlWhiteSpace(((System.Web.UI.WebControls.LinkButton)(gvRow.Cells[1].Controls[0])).Text);
            }
            else
            {
                hdnItemID.Value = string.Empty;
            }
        }

        protected void btnRlsRulesMoveRight_Click(object sender, EventArgs e)
        {
            PayOffRulesEntity payOffRulesEntity = new PayOffRulesEntity();
            List<string> lstErrMsg = new List<string>();
            bool bFlag = false;
            if (drpdwnlstRlsItem.SelectedIndex == -1)
            {
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Must select a Release Item before attaching.');", true);
                return;
            }
            else
            {
                foreach (GridViewRow item in cstGrdRlsPayoffTemp.GridViewPaging.Rows)
                {
                    CheckBox chkRowSelect = (item.Cells[0].FindControl("chkMultipleSelect") as CheckBox);
                    if (chkRowSelect.Checked == true)
                    {
                        bFlag = true;
                        payOffRulesEntity.RuleType = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[1].Text);
                        payOffRulesEntity.RuleID = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[2].Text);
                        payOffRulesEntity.RuleDescription = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[3].Text);
                        payOffRulesEntity.Calc1Desc = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[4].Text);
                        payOffRulesEntity.Calc1Value = (TCLHelper.RemoveHtmlWhiteSpace(item.Cells[5].Text));
                        payOffRulesEntity.Calc1UsePcnt = TCLHelper.ConvertToInt(TCLHelper.RemoveHtmlWhiteSpace(item.Cells[6].Text));
                        payOffRulesEntity.Calc1Operation = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[7].Text);
                        payOffRulesEntity.Calc1Field = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[8].Text);
                        payOffRulesEntity.Calc1FieldLabel = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[9].Text);
                        payOffRulesEntity.Calc1Prompt = TCLHelper.ConvertToInt(TCLHelper.RemoveHtmlWhiteSpace(item.Cells[10].Text));
                        payOffRulesEntity.Calc1Calc2Operation = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[11].Text);
                        payOffRulesEntity.Calc2Desc = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[12].Text);
                        payOffRulesEntity.Calc2Value = (TCLHelper.RemoveHtmlWhiteSpace(item.Cells[13].Text));
                        payOffRulesEntity.Calc2UsePcnt = TCLHelper.ConvertToInt(TCLHelper.RemoveHtmlWhiteSpace(item.Cells[14].Text));
                        payOffRulesEntity.Calc2Operation = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[15].Text);
                        payOffRulesEntity.Calc2Field = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[16].Text);
                        payOffRulesEntity.Calc2FieldLabel = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[17].Text);
                        payOffRulesEntity.Calc2Prompt = TCLHelper.ConvertToInt(TCLHelper.RemoveHtmlWhiteSpace(item.Cells[18].Text));
                        payOffRulesEntity.LOTLOANNUM = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[19].Text);
                        payOffRulesEntity.LOTUNITNUM = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[20].Text);
                        payOffRulesEntity.LOTLOANRELEASE = TCLHelper.RemoveHtmlWhiteSpace(item.Cells[21].Text);
                        //string BNUMBER = item.Cells[22].Text;
                        //string AutoAttach = item.Cells[23].Text;
                        //string RuleEdited = item.Cells[24].Text;
                        payOffRulesEntity.PNOTE = this.NoteNumber;
                        payOffRulesEntity.PUNIT = this.UnitNumber;
                        payOffRulesEntity.RSITEM = drpdwnlstRlsItem.GetSelectedValue();
                        //string RSDESC = item.Cells[28].Text;
                        //string Calc1Result = item.Cells[29].Text;
                        //string Calc2Result = item.Cells[30].Text;
                        //string POQRECID = item.Cells[31].Text;
                        //string POQRULERECID = item.Cells[32].Text;
                        //string RQRECID = item.Cells[33].Text;
                        //string EditedDesc = item.Cells[34].Text;
                        //string LOTLOANNUMBER = item.Cells[35].Text;
                        //string QuotedAmount = item.Cells[36].Text;
                        //string UnknowValues = item.Cells[37].Text;
                        //string EOR = item.Cells[38].Text;
                        string returnMessage = this.noteInfoPresenter.InsertReleaseRules_Temp(payOffRulesEntity);
                        if (string.IsNullOrEmpty(returnMessage) == false)
                        {
                            returnMessage = returnMessage.Replace("^", Environment.NewLine);
                            lstErrMsg.Add(returnMessage);
                        }

                        this.BindAttachedRuleGrid();
                        this.BindReleaseRuleGrid();
                    }
                }
                if (!bFlag)
                {
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('No Rule(s) selected to attach.');", true);
                    return;
                }
            }

            if (lstErrMsg.Count > 0)
            {
                string message = TCLHelper.JavascriptSerializer<List<string>>(lstErrMsg);
                ScriptManager.RegisterStartupScript(Page, this.GetType(), "message", "javascript:messageParse(" + message + ");", true);
            }
        }

        protected void drpdwnlstRlsItem_SelectedIndexChanged(object sender, EventArgs e)
        {
            this.ReleaseItemSelectedValue = drpdwnlstRlsItem.GetSelectedValue();
            this.BindAttachedRuleGrid();
            this.BindReleaseRuleGrid();
        }

        protected void chkRlsRulsShwoAll_CheckedChanged(object sender, EventArgs e)
        {
            if (chkRlsRulsShwoAll.Checked == true)
            {
                this.BindReleaseRuleGrid();
            }
            else
            {
                string selValue = drpdwnlstRlsItem.GetSelectedValue();
                using (DataSet ds = this.noteInfoPresenter.FilterRuleRelease(selValue))
                {
                    if (ds.IsValidDataSet())
                    {
                        cstGrdRlsPayoffTemp.GridRowStyleCSS = "normalrow";
                        cstGrdRlsPayoffTemp.GridHeaderRowCSS = "pl10 pr10 gridheader";
                        cstGrdRlsPayoffTemp.GridAlternatingRowCSS = "altrow";
                        //cstGrdRlsPayoffTemp.GridClientID = "cstGrdRlsPayoffTemp";
                        cstGrdRlsPayoffTemp.GridAllowPaging = false;
                        cstGrdRlsPayoffTemp.GridWidth = Unit.Percentage(100);
                        cstGrdRlsPayoffTemp.ShowColumns = new int[] { 0, 1, 2 };
                        cstGrdRlsPayoffTemp.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Multiple;
                        cstGrdRlsPayoffTemp.DataSource = ds;
                        cstGrdRlsPayoffTemp.BindGrid();
                    }
                }
            }
        }

        protected void grdRlsSch_GridRowEditing(object sender, EventArgs e)
        {
            GridViewRow gvRow = grdRlsSch.SelectedRow;
            LinkButton lnkAttach = (LinkButton)gvRow.FindControl("lnk0");
            string itemno;
            itemno = lnkAttach.Text;//gvRow.Cells[0].Text.ToString();
            sessionProvider.Set("rsitem", itemno);
            string script = "ReleaseRebind('" + itemno + "')";
            InvokeJavascriptFunction(script);
            //  ScriptManager.RegisterStartupScript(Page, this.GetType(), "OpenSingle", "javascript:ReleaseRebind();", true);


        }

        #endregion

        #region Gopi(Financial,Interest,Equiry)

        private void InitializeViewStates()
        {
            if (ViewState["BorrowerNo"] != null && string.IsNullOrEmpty(ViewState["BorrowerNo"].ToString()) == false)
            {
                this.BorrowerNo = ViewState["BorrowerNo"].ToString();
            }
            if (ViewState["dPrevMatDate"] != null && string.IsNullOrEmpty(ViewState["dPrevMatDate"].ToString()) == false)
            {
                this.dPrevMatDate = ViewState["dPrevMatDate"].ToString();
            }

            if (ViewState["blnPostExtFee"] != null && string.IsNullOrEmpty(ViewState["blnPostExtFee"].ToString()) == false)
            {
                this.blnPostExtFee = TCLHelper.ConvertToBool(ViewState["blnPostExtFee"].ToString());
            }

            if (ViewState["bFeePostMaturity"] != null && string.IsNullOrEmpty(ViewState["bFeePostMaturity"].ToString()) == false)
            {
                this.bFeePostMaturity = TCLHelper.ConvertToInt(ViewState["bFeePostMaturity"].ToString());
            }

            if (ViewState["nFeeAmount"] != null && string.IsNullOrEmpty(ViewState["nFeeAmount"].ToString()) == false)
            {
                this.nFeeAmount = TCLHelper.ConvertToDouble(ViewState["nFeeAmount"].ToString());
            }

            if (ViewState["bLOCIntProfAdd"] != null && string.IsNullOrEmpty(ViewState["bLOCIntProfAdd"].ToString()) == false)
            {
                this.bLOCIntProfAdd = TCLHelper.ConvertToBool(ViewState["bLOCIntProfAdd"].ToString());
            }

            if (ViewState["bLOCIntProf"] != null && string.IsNullOrEmpty(ViewState["bLOCIntProf"].ToString()) == false)
            {
                this.bLOCIntProf = TCLHelper.ConvertToBool(ViewState["bLOCIntProf"].ToString());
            }

            if (ViewState["bLOCEqtProfAdd"] != null && string.IsNullOrEmpty(ViewState["bLOCEqtProfAdd"].ToString()) == false)
            {
                this.bLOCEqtProfAdd = TCLHelper.ConvertToBool(ViewState["bLOCEqtProfAdd"].ToString());
            }

            if (ViewState["bLOCEqtProf"] != null && string.IsNullOrEmpty(ViewState["bLOCEqtProf"].ToString()) == false)
            {
                this.bLOCEqtProf = TCLHelper.ConvertToBool(ViewState["bLOCEqtProf"].ToString());
            }

            if (ViewState["mblnLOCProblemOnLoad"] != null && string.IsNullOrEmpty(ViewState["mblnLOCProblemOnLoad"].ToString()) == false)
            {
                this.mblnLOCProblemOnLoad = TCLHelper.ConvertToBool(ViewState["mblnLOCProblemOnLoad"].ToString());
            }

            if (ViewState["dPrvCompDate"] != null && string.IsNullOrEmpty(ViewState["dPrvCompDate"].ToString()) == false)
            {
                this.dPrvCompDate = ViewState["dPrvCompDate"].ToString();
            }

            if (ViewState["Action"] != null && string.IsNullOrEmpty(ViewState["Action"].ToString()) == false)
            {
                this.Action = TCLHelper.ConvertToInt(ViewState["Action"].ToString());
            }

            if (ViewState["bRenewal"] != null && string.IsNullOrEmpty(ViewState["bRenewal"].ToString()) == false)
            {
                this.bRenewal = TCLHelper.ConvertToInt(ViewState["bRenewal"].ToString());
            }

            if (ViewState["bFeePostCompDate"] != null && string.IsNullOrEmpty(ViewState["bFeePostCompDate"].ToString()) == false)
            {
                this.bFeePostCompDate = TCLHelper.ConvertToInt(ViewState["bFeePostCompDate"].ToString());
            }

            if (ViewState["nRenewalCount"] != null && string.IsNullOrEmpty(ViewState["nRenewalCount"].ToString()) == false)
            {
                this.nRenewalCount = TCLHelper.ConvertToInt(ViewState["nRenewalCount"].ToString());
            }

            if (ViewState["sSubLookupIntProf"] != null && string.IsNullOrEmpty(ViewState["sSubLookupIntProf"].ToString()) == false)
            {
                this.sSubLookupIntProf = ViewState["sSubLookupIntProf"].ToString();
            }

            if (ViewState["dblMasterLookupIntProf"] != null && string.IsNullOrEmpty(ViewState["dblMasterLookupIntProf"].ToString()) == false)
            {
                this.dblMasterLookupIntProf = ViewState["dblMasterLookupIntProf"].ToString();
            }

            if (ViewState["prsamt_d"] != null && string.IsNullOrEmpty(ViewState["prsamt_d"].ToString()) == false)
            {
                this.prsamt_d = ViewState["prsamt_d"].ToString();
            }

            if (ViewState["pcfamt"] != null && string.IsNullOrEmpty(ViewState["pcfamt"].ToString()) == false)
            {
                this.pcfamt = ViewState["pcfamt"].ToString();
            }

            if (ViewState["PCLAMT_D"] != null && string.IsNullOrEmpty(ViewState["PCLAMT_D"].ToString()) == false)
            {
                this.PCLAMT_D = ViewState["PCLAMT_D"].ToString();
            }

            if (ViewState["PFDATE"] != null && string.IsNullOrEmpty(ViewState["PFDATE"].ToString()) == false)
            {
                this.PFDATE = ViewState["PFDATE"].ToString();
            }

            if (ViewState["mnPrvNonAccrual"] != null && string.IsNullOrEmpty(ViewState["mnPrvNonAccrual"].ToString()) == false)
            {
                this.mnPrvNonAccrual = TCLHelper.ConvertToBool(ViewState["mnPrvNonAccrual"]);
            }

            if (ViewState["blnAUDITRPT"] != null && string.IsNullOrEmpty(ViewState["blnAUDITRPT"].ToString()) == false)
            {
                this.blnAUDITRPT = TCLHelper.ConvertToBool(ViewState["blnAUDITRPT"]);
            }

            if (ViewState["blnAR_TAXID"] != null && string.IsNullOrEmpty(ViewState["blnAR_TAXID"].ToString()) == false)
            {
                this.blnAR_TAXID = TCLHelper.ConvertToBool(ViewState["blnAR_TAXID"]);
            }

            if (ViewState["blnAR_LDESC"] != null && string.IsNullOrEmpty(ViewState["blnAR_LDESC"].ToString()) == false)
            {
                this.blnAR_LDESC = TCLHelper.ConvertToBool(ViewState["blnAR_LDESC"]);
            }

            if (ViewState["blnAR_LOC"] != null && string.IsNullOrEmpty(ViewState["blnAR_LOC"].ToString()) == false)
            {
                this.blnAR_LOC = TCLHelper.ConvertToBool(ViewState["blnAR_LOC"]);
            }

            if (ViewState["blnAR_LOCMAT"] != null && string.IsNullOrEmpty(ViewState["blnAR_LOCMAT"].ToString()) == false)
            {
                this.blnAR_LOCMAT = TCLHelper.ConvertToBool(ViewState["blnAR_LOCMAT"]);
            }

            if (ViewState["blnAR_INT"] != null && string.IsNullOrEmpty(ViewState["blnAR_INT"].ToString()) == false)
            {
                this.blnAR_INT = TCLHelper.ConvertToBool(ViewState["blnAR_INT"]);
            }

            if (ViewState["blnAR_BILLOPT"] != null && string.IsNullOrEmpty(ViewState["blnAR_BILLOPT"].ToString()) == false)
            {
                this.blnAR_BILLOPT = TCLHelper.ConvertToBool(ViewState["blnAR_BILLOPT"]);
            }

            if (ViewState["blnAR_BUD"] != null && string.IsNullOrEmpty(ViewState["blnAR_BUD"].ToString()) == false)
            {
                this.blnAR_BUD = TCLHelper.ConvertToBool(ViewState["blnAR_BUD"]);
            }

            if (ViewState["blnAR_BUDPROF"] != null && string.IsNullOrEmpty(ViewState["blnAR_BUDPROF"].ToString()) == false)
            {
                this.blnAR_BUDPROF = TCLHelper.ConvertToBool(ViewState["blnAR_BUDPROF"]);
            }

            if (ViewState["blnAR_EQTPROF"] != null && string.IsNullOrEmpty(ViewState["blnAR_EQTPROF"].ToString()) == false)
            {
                this.blnAR_EQTPROF = TCLHelper.ConvertToBool(ViewState["blnAR_EQTPROF"]);
            }

            if (ViewState["blnAR_LOCPARENTTOTAL"] != null && string.IsNullOrEmpty(ViewState["blnAR_LOCPARENTTOTAL"].ToString()) == false)
            {
                this.blnAR_LOCPARENTTOTAL = TCLHelper.ConvertToBool(ViewState["blnAR_LOCPARENTTOTAL"]);
            }

            if (ViewState["blnAR_LOCTERMS"] != null && string.IsNullOrEmpty(ViewState["blnAR_LOCTERMS"].ToString()) == false)
            {
                this.blnAR_LOCTERMS = TCLHelper.ConvertToBool(ViewState["blnAR_LOCTERMS"]);
            }

            if (ViewState["cAlloc"] != null && string.IsNullOrEmpty(ViewState["cAlloc"].ToString()) == false)
            {
                this.cAlloc = TCLHelper.ConvertToDouble(ViewState["cAlloc"]);
            }

            if (ViewState["cEst"] != null && string.IsNullOrEmpty(ViewState["cEst"].ToString()) == false)
            {
                this.cEst = TCLHelper.ConvertToDouble(ViewState["cEst"]);
            }

            if (ViewState["cDiff"] != null && string.IsNullOrEmpty(ViewState["cDiff"].ToString()) == false)
            {
                this.cDiff = TCLHelper.ConvertToDouble(ViewState["cDiff"]);
            }
        }

        protected void imgbtnBdgtCntrlAdd_Click(object sender, ImageClickEventArgs e)
        {
            lblNoteNo.Text = this.NoteNumber;
            lblUnitNumber.Text = this.UnitNumber;
            lblBudgetId.Text = Convert.ToString(ddlBudgets.SelectedItem.Text);
            txtGroupDesc.Text = "";
            BindBudgetNotes(0);
            if (string.IsNullOrEmpty(ddlBudgets.SelectedValue) == true)
            {
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Please select a Budget Group.');", true);
                return;
            }

            mpeAddBudget.Show();
        }

        private void GetEquityProfileGrid()
        {
            imgbtEqtyPrflsCopy.Enabled = false;
            imgbtEqtyPrflsDel.Enabled = false;
            using (DataSet dsEquityProfile = this.noteInfoPresenter.LoadEquityProfileGrid())
            {
                if (dsEquityProfile.IsValidDataColumn() == true)
                {
                    hdnEPEffDate.Value = string.Empty;
                    CGEquityProfile.GridRowStyleCSS = "normalrow";
                    CGEquityProfile.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    CGEquityProfile.GridAlternatingRowCSS = "altrow";
                    CGEquityProfile.GridViewPaging.ShowHeader = true;
                    CGEquityProfile.GridAllowPaging = false;
                    CGEquityProfile.AllowLinks = new int[] { 4 };
                    CGEquityProfile.DataKeyNames = new string[] { "EFF DATE" };
                    //CGEquityProfile.GridWidth = Unit.Percentage(100);
                    CGEquityProfile.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                    CGEquityProfile.DataSource = dsEquityProfile;
                    CGEquityProfile.BindGrid();
                    if (dsEquityProfile.IsValidDataSet())
                    {
                        imgbtEqtyPrflsCopy.Enabled = true;
                        imgbtEqtyPrflsDel.Enabled = true;
                    }
                }
            }
        }

        private void GetIntrestProfileGrid()
        {
            imgbtnIntrstPrflsDel.Enabled = false;
            imgbtnIntrstPrflsCopy.Enabled = false;
            using (DataSet dsInterestProf = this.noteInfoPresenter.LoadIntrestProfileGrid())
            {
                if (dsInterestProf.IsValidDataColumn() == true)
                {
                    hdnIPEffDate.Value = string.Empty;
                    CGIntrestProfile.GridRowStyleCSS = "normalrow";
                    CGIntrestProfile.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    CGIntrestProfile.GridAlternatingRowCSS = "altrow";
                    CGIntrestProfile.GridViewPaging.ShowHeader = true;
                    CGIntrestProfile.GridAllowPaging = false;
                    CGIntrestProfile.AllowLinks = new int[] { 1 };
                    CGIntrestProfile.HideColumns = new int[] { 30 };
                    CGIntrestProfile.DataKeyNames = new string[] { "IEFFDATE" };
                    //CGIntrestProfile.GridWidth = Unit.Percentage(100);
                    CGIntrestProfile.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                    CGIntrestProfile.DataSource = dsInterestProf;
                    CGIntrestProfile.BindGrid();
                    if (dsInterestProf.IsValidDataSet())
                    {
                        imgbtnIntrstPrflsDel.Enabled = true;
                        imgbtnIntrstPrflsCopy.Enabled = true;
                    }
                }
            }
        }

        //private void ShowMessage()
        //{
        //    string strMsg = string.Format("This Will Remove the Highlighted Interest Profile");
        //    ScriptManager.RegisterStartupScript(this, this.GetType(), "confirm", "ValidateRate1('" + strMsg + "');", true);
        //}

        protected void IPImgbtnDelete_Click(object sender, ImageClickEventArgs e)
        {

            if (string.IsNullOrEmpty(hdnIPEffDate.Value) == false)
            {
                this.EffDate = Convert.ToString(hdnIPEffDate.Value);
                //ShowMessage();
                this.noteInfoPresenter.DeleteIntrestProfile();
                GetIntrestProfileGrid();
                tblMsg.Style.Add("display", "block");
                ErrorSuccess.Style.Add("display", "block");
                lblErrorSuccess.Text = "Record deleted successfully.";
            }
            else
            {
                ErrorFail.Visible = true;
                lblErrorFail.Text = "Please Select a Row to delete.";
            }
        }

        protected void imgbtEqtyPrflsDel_Click(object sender, ImageClickEventArgs e)
        {
            if (string.IsNullOrEmpty(hdnEPEffDate.Value) == false)
            {
                this.EffDate = Convert.ToString(hdnEPEffDate.Value);
                this.EQtype = Convert.ToString(hdnEPEQtype.Value);
                this.BudgetID = Convert.ToString(hdnEPBudgetID.Value);
                this.noteInfoPresenter.DeleteEquityProfile();
                GetEquityProfileGrid();
            }
        }

        protected void CGIntrestProfile_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            try
            {
                GridViewRow gvRow = CGIntrestProfile.SelectedRow;
                ImageButton SelectUnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
                if (SelectUnSelect.AlternateText == "1")
                {
                    hdnIPEffDate.Value = TCLHelper.GetData(((LinkButton)gvRow.Cells[2].Controls[0]).Text);
                }
                else
                {
                    hdnIPEffDate.Value = string.Empty;
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
                throw;
            }
        }

        protected void CGEquityProfile_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            try
            {
                GridViewRow gvRow = CGEquityProfile.SelectedRow;
                ImageButton SelectUnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
                if (SelectUnSelect.AlternateText == "1")
                {
                    hdnEPEffDate.Value = TCLHelper.GetData(((LinkButton)gvRow.Cells[5].Controls[0]).Text);
                    hdnEPEQtype.Value = TCLHelper.GetData(gvRow.Cells[4].Text);
                    hdnEPBudgetID.Value = TCLHelper.GetData(gvRow.Cells[3].Text);
                }
                else
                {
                    hdnEPEffDate.Value = string.Empty;
                    hdnEPEQtype.Value = string.Empty;
                    hdnEPBudgetID.Value = string.Empty;
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
                throw;
            }
        }

        protected void chkORComRule_Changed(object sender, EventArgs e)
        {
            mblnComRuleOverride = chkORComRule.Checked;
            if (!mblnComRuleNoUpdate)
            {
                if (chkORComRule.Tag != Convert.ToString(chkORComRule.Checked))
                    mblnComRuleChanged = true;
                if (this.noteInfoPresenter.ComRuleValidate())
                {

                }
            }
            this.noteInfoPresenter.ComRulesApply(); // Use apply to Set it
        }

        protected void btnFincTabPostFee_Click(object sender, EventArgs e)
        {
            string glCode = ddlGLTable.GetSelectedValue();
            if (string.IsNullOrEmpty(glCode) == false)
            {
                //frmFeePost.Show(vbModal);                    
                return;
            }
            else
            {
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Please select a GL Table.  Required for transaction codes in fee posting');", true);
                return;
            }
        }

        public void NoteinfoLoad(DataSet dsLoad)
        {
            try
            {	// On Error GoTo SetupLoadError
                bool blnMstrLOCFound;
                mblnInitLoad = true;
                blnMstrLOCFound = false;
                mblnFirstTime = true;
                MasterSubLOC MasterSubLOC = new MasterSubLOC();
                NoteInfoType NoteInfoType = new NoteInfoType();
                using (DataSet ds = this.noteInfoPresenter.BorrowerCheck())
                {
                    if (ds.IsValidDataSet() == false)
                    {
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alert", "alert('Borrower not found: '" + this.BorrowerNo, true);
                        btnProjectSave.Visible = false;
                        return;
                    }

                    this.bLOCIntProf = false;
                    bLOCIntProfAdd = false;
                    sSubLookupIntProf = "";
                    this.dblMasterLookupIntProf = "0";
                    this.bLOCEqtProf = false;
                    this.bLOCEqtProfAdd = false;

                    //start coding
                    if (this.Action == 1)
                    {
                        if (MasterSubLOC.LOCType == "P")
                        {
                            mintLTOBLOC = 1;
                        }
                        else if (MasterSubLOC.LOCType == "C")
                        {
                            mintLTOBLOC = 2;
                        }
                        else
                        {
                            mintLTOBLOC = 0;
                        }
                        this.ParentNo = TCLHelper.GetData(MasterSubLOC.ParentNO);
                    }
                    else
                    {
                        this.mintLTOBLOC = TCLHelper.ConvertToInt(TCLHelper.GetData(ds.Tables[0].Rows[0]["LTOBLOCTYPE"]));
                        this.ParentNo = TCLHelper.GetData(ds.Tables[0].Rows[0]["PARENTNO"]);
                    }
                }
                if (TCLHelper.GetData(this.ParentNo) == String.Empty && (mintLTOBLOC == 2 | MasterSubLOC.LOCType == "C"))
                {
                    if (this.ParentNo != TCLHelper.GetData(MasterSubLOC.ParentNO))
                    {
                        this.ParentNo = TCLHelper.GetData(MasterSubLOC.ParentNO);
                        if (MasterSubLOC.LOCType == "P")
                        {
                            mintLTOBLOC = 1;
                        }
                        else if (MasterSubLOC.LOCType == "C")
                        {
                            mintLTOBLOC = 2;
                        }
                        else
                        {
                            mintLTOBLOC = 0;
                        }
                    }
                }

                if (dsLoad.IsValidDataSet())
                {
                    this.mcurOrig_Commit = TCLHelper.ConvertToDouble(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PCLAMT"]));
                    this.mblnComRuleOverride = TCLHelper.ConvertToTCLBool(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["RuleOverrideFlag"]));
                    this.mdblCommitmentRule = TCLHelper.ConvertToDouble(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["CommitmentRuleID"]));
                    this.nRenewalCount = TCLHelper.ConvertToInt(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PRENEW"]));
                    this.sSubLookupIntProf = TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PLCSEQ"]); // save this one so we know if it changed
                    this.dblMasterLookupIntProf = TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["LOCMID"]);
                    NoteInfoType.NoteFlag = TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PMFLAG"]); // set the note flag so we can disable some stuff

                    //FoundLOCIntProf(TCLHelper.GetData(adoSetupModTable("PBNUMBER")), dblMasterLookupIntProf, sSubLookupIntProf, pubGetDateLocalized, bLOCIntProfAdd);
                    this.bLOCIntProf = this.noteInfoPresenter.FoundLocIntProf(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PBNUMBER"]), TCLHelper.ConvertToDouble(this.dblMasterLookupIntProf), sSubLookupIntProf, TCLHelper.ConvertToBool(this.bLOCIntProfAdd));

                    //FoundLOCEqtProf(TCLHelper.GetData(adoSetupModTable("PBNUMBER")), dblMasterLookupIntProf, sSubLookupIntProf, pubGetDateLocalized, bLOCEqtProfAdd);
                    this.bLOCEqtProf = this.noteInfoPresenter.FoundLocEqtProf(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PBNUMBER"]), TCLHelper.ConvertToDouble(this.dblMasterLookupIntProf), sSubLookupIntProf, TCLHelper.ConvertToBool(this.bLOCEqtProfAdd));

                    if (blnMstrLOCFound == false)
                    {
                        if (TCLHelper.ConvertToInt(dsLoad.Tables[0].Rows[0]["LOCMID"]) > 0)
                        {
                            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alert", "alert('Master LOC attached to this note is no longer available, Problem with Master LOC')", true);
                            this.mblnLOCProblemOnLoad = true;
                            ddlMLoc.SelectedIndex = 0; // Set it to NONE, Not 'Not Attached'
                        }
                        else
                        {
                            ddlMLoc.SelectedIndex = 0;
                        }
                    }
                    else
                    {
                        if (ddlMLoc.Items.Count > 0)
                        {
                            if (ddlSLoc.SelectedIndex < 0)
                            {
                                if (TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PLCSEQ"]) != string.Empty)
                                {
                                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alert", "alert('Sub LOC attached to this note is no longer available, Problem with Sub LOC')", true);
                                    this.mblnLOCProblemOnLoad = true;
                                    ddlSLoc.SelectedIndex = 0; // Set it to NONE, Not 'Not Attached'
                                }
                            }
                        }
                        else
                        {
                            if (TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PLCSEQ"]) != "")
                            {
                                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alert", "alert('Sub LOC attached to this note is no longer available, Problem with Sub LOC')", true);
                                this.mblnLOCProblemOnLoad = true;
                                ddlSLoc.SelectedIndex = 0; // Set it to NONE, Not 'Not Attached'
                            }
                        }
                    }
                    this.bRenewal = 0;
                    this.nRenewalCount = TCLHelper.ConvertToInt(TCLHelper.GetData(dsLoad.Tables[0].Rows[0]["PRENEW"]));
                }
            }
            catch
            {	// SetupLoadError:

            }
        }

        protected void csKeyContacts_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            if (TCLHelper.GetData(ViewState["KeyContEdit"]).Equals(keyContEditFalse, StringComparison.OrdinalIgnoreCase) == true)
                return;
            GridViewRow gvRow = csKeyContacts.SelectedRow;
            ImageButton imgbtnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
            if (imgbtnSelect.AlternateText == "1")
                btnKeyCntsMoveRight.Enabled = true;
            else
                btnKeyCntsMoveRight.Enabled = false;
        }

        protected void csKeyContactAttached_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            if (TCLHelper.GetData(ViewState["KeyContEdit"]).Equals(keyContEditFalse, StringComparison.OrdinalIgnoreCase) == true)
                return;
            GridViewRow gvRow = csKeyContactAttached.SelectedRow;
            ImageButton imgbtnSelect = (ImageButton)gvRow.FindControl("imgRowSelect");
            if (imgbtnSelect.AlternateText == "1")
                imgbtnDKeyContact.Visible = true;
            else
                imgbtnDKeyContact.Visible = false;
        }

        #endregion

        #region Gokul(General,NotePayOff,KeyContacts,BudgetControl)

        private void BindGeneral()
        {
            try
            {
                using (DataSet dsGeneral = noteInfoPresenter.GetNotesGeneral(this.BorrowerNo, this.UserName))
                {
                    //Bind Company
                    if (dsGeneral.Tables.Count > 0)
                    {
                        ddlCompany.DataSource = dsGeneral.Tables[0];
                        ddlCompany.DataValueField = "ID";
                        ddlCompany.DataTextField = "NAME";
                        ddlCompany.DataBind();
                    }

                    //Bind Area
                    if (dsGeneral.Tables.Count > 1)
                    {
                        ddlArea.DataSource = dsGeneral.Tables[1];
                        ddlArea.DataValueField = "ID";
                        ddlArea.DataTextField = "NAME";
                        ddlArea.DataBind();
                    }

                    // Bind M-Class
                    if (dsGeneral.Tables.Count > 2)
                    {
                        ddlMClass.DataSource = dsGeneral.Tables[2];
                        ddlMClass.DataValueField = "PRJMCLASS";
                        ddlMClass.DataTextField = "PRJDESC";
                        ddlMClass.DataBind();
                    }

                    //Bind GL Table
                    if (dsGeneral.Tables.Count > 3)
                    {
                        ddlGLTable.DataSource = dsGeneral.Tables[3];
                        ddlGLTable.DataValueField = "TABLE1";
                        ddlGLTable.DataTextField = "TABLE1";
                        ddlGLTable.DataBind();
                    }

                    //Bind Status 
                    if (dsGeneral.Tables.Count > 4)
                    {

                        ddlStatus.DataSource = dsGeneral.Tables[4];
                        ddlStatus.DataValueField = "CODE";
                        ddlStatus.DataTextField = "DFTVAL";
                        ddlStatus.DataBind();
                    }

                    //Federal Code Status 
                    if (dsGeneral.Tables.Count > 5)
                    {
                        ddlFederalCode.DataSource = dsGeneral.Tables[5];
                        ddlFederalCode.DataValueField = "CODE";
                        ddlFederalCode.DataTextField = "DFTVAL";
                        ddlFederalCode.DataBind();
                    }

                    //Loan Grade
                    if (dsGeneral.Tables.Count > 6)
                    {
                        ddlLoanGrade.DataSource = dsGeneral.Tables[6];
                        ddlLoanGrade.DataValueField = "CODE";
                        ddlLoanGrade.DataTextField = "DFTVAL";
                        ddlLoanGrade.DataBind();
                    }

                    // Loan Class
                    if (dsGeneral.Tables.Count > 7)
                    {
                        ddlLoanClass.DataSource = dsGeneral.Tables[7];
                        ddlLoanClass.DataValueField = "CODE";
                        ddlLoanClass.DataTextField = "DFTVAL";
                        ddlLoanClass.DataBind();
                    }

                    // Loan Type
                    if (dsGeneral.Tables.Count > 8)
                    {
                        ddlLoanType.DataSource = dsGeneral.Tables[8];
                        ddlLoanType.DataValueField = "CODE";
                        ddlLoanType.DataTextField = "DFTVAL";
                        ddlLoanType.DataBind();
                    }

                    // Loan Purpose
                    if (dsGeneral.Tables.Count > 9)
                    {
                        ddlLoanPurpose.DataSource = dsGeneral.Tables[9];
                        ddlLoanPurpose.DataValueField = "CODE";
                        ddlLoanPurpose.DataTextField = "DFTVAL";
                        ddlLoanPurpose.DataBind();
                    }

                    // Collateral Code
                    if (dsGeneral.Tables.Count > 10)
                    {
                        ddlCollateralCode.DataSource = dsGeneral.Tables[10];
                        ddlCollateralCode.DataValueField = "CODE";
                        ddlCollateralCode.DataTextField = "DFTVAL";
                        ddlCollateralCode.DataBind();
                    }

                    // Master LOC
                    if (dsGeneral.Tables.Count > 11)
                    {
                        ddlMLoc.DataSource = dsGeneral.Tables[11];
                        ddlMLoc.DataValueField = "LOCMID";
                        ddlMLoc.DataTextField = "LCDESC";
                        ddlMLoc.DataBind();
                    }

                    //Budgets
                    if (dsGeneral.Tables.Count > 12)
                    {
                        ddlBudgets.DataSource = dsGeneral.Tables[12];
                        ddlBudgets.DataValueField = "STDID";
                        ddlBudgets.DataTextField = "STDDESC";
                        ddlBudgets.DataBind();

                    }

                    //Inspection Company
                    if (dsGeneral.Tables.Count > 13)
                    {
                        ddlInspCompany.DataSource = dsGeneral.Tables[13];
                        ddlInspCompany.DataValueField = "COMPANYID";
                        ddlInspCompany.DataTextField = "COMPANYNAME";
                        ddlInspCompany.DataBind();
                    }

                    //Key Contacts
                    if (dsGeneral.Tables.Count > 14)
                    {
                        ddlKeyContacts.DataSource = dsGeneral.Tables[14];
                        ddlKeyContacts.DataValueField = "BCHMCLASS";
                        ddlKeyContacts.DataTextField = "BCHDESC";
                        ddlKeyContacts.DataBind();
                    }

                    if (ddlKeyContacts.SelectedIndex > -1)
                    {
                        this.BindKeyContacts();
                        this.BindAttachedKeyContacts("", "", "");
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void ddlCompany_SelectedIndexChanged(object sender, EventArgs e)
        {
            try
            {
                if (ddlCompany.SelectedIndex > 0)
                {
                    BindBranch();
                }
                else if (ddlCompany.SelectedIndex == 0)
                {
                    ddlBranch.Items.Clear();
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindBranch()
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                DataTable dtBranch = noteInfoPresenter.GetBranch(ddlCompany.SelectedValue, this.UserName);
                ddlBranch.Items.Clear();
                ddlBranch.DataSource = dtBranch;
                ddlBranch.DataTextField = "NAME";
                ddlBranch.DataValueField = "ID";
                ddlBranch.DataBind();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindLocale()
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                DataTable dtLocale = noteInfoPresenter.GetLocale(ddlArea.SelectedValue);
                ddlLocal.DataSource = dtLocale;
                ddlLocal.DataTextField = "NAME";
                ddlLocal.DataValueField = "ID";
                ddlLocal.DataBind();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindLClass()
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                DataTable dtSClass = noteInfoPresenter.GetSClass(ddlMClass.SelectedValue);
                ddlSClass.DataSource = dtSClass;
                ddlSClass.DataTextField = "NAME";
                ddlSClass.DataValueField = "ID";
                ddlSClass.DataBind();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindSLoc()
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                DataTable dtSClass = noteInfoPresenter.GetSLoc(TCLHelper.ConvertToDouble(ddlMLoc.SelectedValue).ToString());
                ddlSLoc.DataSource = dtSClass;
                ddlSLoc.DataTextField = "LCDESC";
                ddlSLoc.DataValueField = "LCSEQ";
                ddlSLoc.DataBind();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void ddlArea_SelectedIndexChanged(object sender, EventArgs e)
        {
            try
            {
                if (ddlArea.SelectedIndex > 0)
                {
                    BindLocale();
                }
                else if (ddlArea.SelectedIndex == 0)
                {
                    ddlLocal.Items.Clear();
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void ddlMClass_SelectedIndexChanged(object sender, EventArgs e)
        {
            try
            {
                if (ddlMClass.SelectedIndex > 0)
                {
                    BindLClass();
                }
                else if (ddlMClass.SelectedIndex == 0)
                {
                    ddlSClass.Items.Clear();
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void ddlMLoc_SelectedIndexChanged(object sender, EventArgs e)
        {
            try
            {
                if (ddlMLoc.SelectedIndex > 0)
                {
                    BindSLoc();
                }
                else if (ddlMLoc.SelectedIndex == 0)
                {
                    ddlSLoc.Items.Clear();
                    ddlSLoc.Items.Insert(0, new ListItem("Not Attached", ""));
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void GetGeneralNotes()
        {
            try
            {
                bool boolNoteMode = false;
                if (this.NoteMode.ToString().ToUpper() != "Pipeline".ToString().ToUpper())
                    boolNoteMode = true;

                GetProjectDetails = noteInfoPresenter.GetGeneralNotes(NoteNumber, UnitNumber, this.BorrowerNo, boolNoteMode);

                if (ddlCompany.Items.FindByValue(GetProjectDetails.Company) != null)
                {
                    ddlCompany.SelectedValue = GetProjectDetails.Company;
                    if (ddlCompany.SelectedIndex > 0)
                        BindBranch();
                }

                if (ddlBranch.Items.FindByValue(GetProjectDetails.Branch) != null)
                    ddlBranch.SelectedValue = GetProjectDetails.Branch;

                if (ddlArea.Items.FindByValue(GetProjectDetails.Area) != null)
                {
                    ddlArea.SelectedValue = GetProjectDetails.Area;
                    if (ddlArea.SelectedIndex > 0)
                        BindLocale();
                }

                if (ddlLocal.Items.FindByValue(GetProjectDetails.Locale) != null)
                    ddlLocal.SelectedValue = GetProjectDetails.Locale;

                if (ddlMClass.Items.FindByValue(GetProjectDetails.MClass) != null)
                {
                    ddlMClass.SelectedValue = GetProjectDetails.MClass;
                    if (ddlMClass.SelectedIndex > 0)
                        BindLClass();
                }

                if (ddlSClass.Items.FindByValue(GetProjectDetails.SClass) != null)
                    ddlSClass.SelectedValue = GetProjectDetails.SClass;

                if (ddlMLoc.Items.FindByValue(GetProjectDetails.MLoc) != null)
                    ddlMLoc.SelectedValue = GetProjectDetails.MLoc;

                if (ddlMLoc.SelectedIndex == 0)
                    ddlSLoc.Items.Insert(0, new ListItem("Not Attached", ""));
                else
                    BindSLoc();

                if (ddlSLoc.Items.FindByValue(GetProjectDetails.SLoc) != null)
                    ddlSLoc.SelectedValue = GetProjectDetails.SLoc;

                chkRevolving.Checked = GetProjectDetails.Revolving == "Y" ? true : false;

                //chkFannieMae.Checked = GetProjectDetails.FannieMae == 0 ? false : true;


                //if (chkRevolving.Checked)
                //{
                //    chkFannieMae.Checked = false;
                //    chkFannieMae.Enabled = false;
                //}
                //if (chkFannieMae.Checked)
                //{
                //    chkRevolving.Checked = false;
                //    chkRevolving.Enabled = false;
                //}

                chkNonAccural.Checked = GetProjectDetails.NonAccural == 0 ? false : true;
                chkInDefault.Checked = GetProjectDetails.InDefault == 0 ? false : true;
                chkStopFin.Checked = GetProjectDetails.StopFinActivity == 0 ? false : true;
                chkForeclosure.Checked = GetProjectDetails.Foreclosure == 0 ? false : true;
                chkBankruptcy.Checked = GetProjectDetails.Bankruptcy == 0 ? false : true;
                chk203K.Checked = GetProjectDetails.TwoNotthreeK == 0 ? false : true;
                chkRollToPerm.Checked = GetProjectDetails.RollToPerm == 0 ? false : true;
                chkAssetManagementt.Checked = GetProjectDetails.AssetManagement == 0 ? false : true;

                //chkAmortizeLoan.Checked = GetProjectDetails.AmortizeLoan == 0 ? false : true;
                //if (chkAmortizeLoan.Checked == true)
                //{
                //    chkAutomatic.Checked = GetProjectDetails.AutomaticRecast == 0 ? false : true;
                //    chkOriginal.Checked = GetProjectDetails.OriginalTerms == 0 ? false : true;
                //}
                //else
                //{
                //    chkAutomatic.Checked = false;
                //    chkOriginal.Checked = false;
                //    chkAutomatic.Enabled = false;
                //    chkOriginal.Enabled = false;
                //}
                ddlGLTable.SetSelectedText(GetProjectDetails.GLTable);
                ddlStatus.SetSelectedText(GetProjectDetails.Status);
                ddlFederalCode.SetSelectedText(GetProjectDetails.FederalCode);
                ddlLoanGrade.SetSelectedText(GetProjectDetails.LoanGrade);
                ddlLoanClass.SetSelectedText(GetProjectDetails.LoanClass);
                ddlLoanType.SetSelectedText(GetProjectDetails.LoanType);
                ddlLoanPurpose.SetSelectedText(GetProjectDetails.LoanPurpose);
                ddlCollateralCode.SetSelectedText(GetProjectDetails.CollateralCode);

                txtLoanGrdDate.Text = Convert.ToString(GetProjectDetails.LoanGradeDate);
                txtCensusTest.Text = Convert.ToString(GetProjectDetails.CensusTest);
                txtCommitment.Text = Convert.ToString(GetProjectDetails.Commitment);

                txtBudgetCommitment.Text = Convert.ToString(GetProjectDetails.BudgetCommitment);
                txtTotalEstimated.Text = Convert.ToString(GetProjectDetails.TotalEstimated);
                txtAlctCommit.Text = Convert.ToString(GetProjectDetails.AllocatedCommitement);
                txtTotalAllocated.Text = Convert.ToString(GetProjectDetails.TotalAllocated);
                chkOmit.Checked = GetProjectDetails.BudgetOmit == 0 ? false : true; //OmitBVOnWebInspFlag
                chkOutside.Checked = GetProjectDetails.BudgetOutSide == "Y" ? true : false; //OutsideLast

                ddlAutoGenBrwFndFirst.SetSelectedValue(GetProjectDetails.BorrowerFund);
                ddlInspCompany.SetSelectedValue(GetProjectDetails.CompanyId);
                ddlBudgets.SetSelectedValue(GetProjectDetails.BudgetId);
                if (ddlBudgets.Items.FindByValue(GetProjectDetails.BudgetId) != null)
                {
                    ddlBudgets.SelectedValue = GetProjectDetails.BudgetId;
                    hdnBudget.Value = ddlBudgets.SelectedValue;
                    BindBudgetNotes(0);
                    if (string.IsNullOrEmpty(ddlBudgets.SelectedValue) == false)
                        lblBudgetTitle.Text = Convert.ToString(GetProjectDetails.BudgetDesc);

                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindBudgetNotes(int intMode)
        {
            noteInfoPresenter = new NoteInfoPresenter(this);
            using (DataSet dsBudget = noteInfoPresenter.GetBudgetNotes(NoteNumber, UnitNumber, ddlBudgets.SelectedValue, intMode, chk203K.Checked == false ? 0 : -1))
            {
                if (dsBudget.IsValidDataColumn() == true)
                {
                    cgBudget.GridClientID = "cgBudget";
                    cgBudget.DataSource = dsBudget;
                    cgBudget.GridRowStyleCSS = "normalrow";
                    cgBudget.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    cgBudget.GridAlternatingRowCSS = "altrow";
                    cgBudget.HideColumns = new int[] { 2, 3, 4, 5 };
                    cgBudget.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                    cgBudget.GridWidth = Unit.Percentage(100);
                    cgBudget.GridAllowPaging = false;
                    cgBudget.BindGrid();

                    if (dsBudget.Tables.Count > 1 && dsBudget.Tables[1].Rows.Count > 0)
                    {

                        int intGroupId = TCLHelper.ConvertToInt(dsBudget.Tables[1].Rows[0]["MAXITEM"]) + 1;
                        txtGroupID.Text = intGroupId.ToString("D2");
                    }

                    if (dsBudget.Tables.Count > 2)
                    {
                        CalcBudget(dsBudget);
                    }
                }
            }
        }
        private void CalcBudget(DataSet dsBudget)
        {
            double dblAllocated = 0;
            double dblTotalAllocated = 0;
            if (dsBudget.Tables[2].Rows.Count > 0)
            {
                for (int intI = 0; intI < dsBudget.Tables[2].Rows.Count; intI++)
                {
                    dblAllocated = dblAllocated + TCLHelper.ConvertToDouble(dsBudget.Tables[2].Rows[intI]["BCCOST"]) + TCLHelper.ConvertToDouble(dsBudget.Tables[2].Rows[intI]["BCEQUITY"]);
                    dblTotalAllocated = dblTotalAllocated + TCLHelper.ConvertToDouble(dsBudget.Tables[2].Rows[intI]["BCCOST"]);
                }
            }

            if (dsBudget.Tables[0].Rows.Count > 0)
            {
                if (dsBudget.Tables[0].Rows.Count > 0)
                {
                    for (int intI = 0; intI < dsBudget.Tables[0].Rows.Count; intI++)
                    {
                        if (Convert.ToString(dsBudget.Tables[0].Rows[intI]["BCID"]) + Convert.ToString(dsBudget.Tables[0].Rows[intI]["BCLV1"]) + Convert.ToString(dsBudget.Tables[0].Rows[intI]["BCLV2"]) == "9999900")
                        {
                            dblAllocated = dblAllocated + TCLHelper.ConvertToDouble(Convert.ToString(txtFincTabConstAdjsmnt.Text).Replace("$", "").Replace(",", ""));
                            dblTotalAllocated = dblTotalAllocated + TCLHelper.ConvertToDouble(Convert.ToString(txtFincTabConstAdjsmnt.Text).Replace("$", "").Replace(",", ""));
                        }
                    }

                }
            }

            if (dblAllocated > 0)
                txtAlctCommit.Text = TCLHelper.ConvertToUSCurrency(dblAllocated);
            else
                txtAlctCommit.Text = "";

            if (dblTotalAllocated > 0)
                txtTotalAllocated.Text = TCLHelper.ConvertToUSCurrency(dblTotalAllocated);
            else
                txtTotalAllocated.Text = "";


        }

        protected void ImgbtnDelete_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRow in cgBudget.GridViewPaging.Rows)
                {
                    ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                    if (selectButton.AlternateText == "1")
                    {
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "DeleteBudget('Are you sure you want to delete the selected budget group(s) for this loan?');", true);
                        return;

                    }
                }
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('No Groups Selected');", true);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnDeleteBudget_Click(object sender, EventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRow in cgBudget.GridViewPaging.Rows)
                {
                    ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                    if (selectButton.AlternateText == "1")
                    {
                        string BCID = Convert.ToString(gvRow.Cells[1].Text);
                        if (BCID == "99")
                        {
                            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('99 - General Draw Line Item cannot be deleted.\\n\\nContinuing to Process...?');", true);
                            return;
                        }

                        string Id = Convert.ToString(gvRow.Cells[3].Text);
                        string BCLV1 = Convert.ToString(gvRow.Cells[4].Text);
                        string BCLV2 = Convert.ToString(gvRow.Cells[5].Text);
                        string BCTYPE = Convert.ToString(gvRow.Cells[6].Text);

                        long intCalc;
                        noteInfoPresenter = new NoteInfoPresenter(this);
                        noteInfoPresenter.GetBudgetCalc(NoteNumber, UnitNumber, Id, BCLV1, out intCalc);

                        if (intCalc == 0)
                        {
                            noteInfoPresenter = new NoteInfoPresenter(this);
                            noteInfoPresenter.DeleteBudget(NoteNumber, UnitNumber, Id, BCLV1, BCLV2, BCTYPE);
                            BindBudgetNotes(0);
                            tblMsgMPopup.Visible = true;
                            trAlertSuccess.Visible = true;
                            lblSuccess.Text = "Group ID deleted sucessfully";
                            lblSuccess.Visible = true;
                            ErrorAlert1.Visible = false;
                            lblErrorAlert.Visible = false;
                            lblErrorAlert.Text = string.Empty;
                        }
                        else
                        {
                            string strMsg = string.Empty;
                            strMsg = "Budget Group(s) " + Convert.ToString(gvRow.Cells[4].Text) + " have Receipts/Disbursements or Inspections posted Cannot change budgets.";
                            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('" + strMsg + "');", true);
                            return;
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnSelectBudget_Click(object sender, EventArgs e)
        {
            try
            {
                if (Convert.ToString(hdnBudgetTemp.Value) != "1")
                {


                    string strCheck = string.Empty;
                    tblMsgMPopup.Visible = false;
                    noteInfoPresenter = new NoteInfoPresenter(this);
                    using (DataSet dsBudget = noteInfoPresenter.CheckBudget(NoteNumber, UnitNumber))
                    {
                        if (TCLHelper.IsValidDataColumn(dsBudget))
                        {
                            if (dsBudget.Tables[0].Rows.Count > 0)
                            {
                                strCheck = Convert.ToString(dsBudget.Tables[0].Rows[0]["Result"]);
                            }
                        }
                    }
                    if (strCheck == "0")
                    {
                        hdnBudget.Value = ddlBudgets.SelectedValue;
                        BindBudgetNotes(1);
                        if (string.IsNullOrEmpty(ddlBudgets.SelectedValue) == false)
                        {
                            lblBudgetTitle.Text = Convert.ToString(ddlBudgets.SelectedItem.Text);
                        }
                        else
                        {
                            lblBudgetTitle.Text = "";
                        }
                    }
                    else
                    {
                        string strMsg = string.Empty;
                        if (ddlBudgets.Items.FindByValue(Convert.ToString(hdnBudget.Value)) != null)
                            ddlBudgets.SelectedValue = Convert.ToString(hdnBudget.Value);
                        strMsg = "Budget Group(s) " + strCheck + " have Receipts/Disbursements or Inspections posted Cannot change budgets.";
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('" + strMsg + "');", true);
                        return;
                    }
                }
                else
                {
                    BindBudgetNotes(1);
                    hdnBudgetTemp.Value = "";
                }

            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindKeyContacts()
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                using (DataSet dsBudget = noteInfoPresenter.GetKeyContact(ddlKeyContacts.SelectedValue, Convert.ToString(txtFindContact.Text)))
                {
                    if (dsBudget.IsValidDataColumn())
                    {
                        csKeyContacts.GridClientID = "csKeyContacts";
                        csKeyContacts.DataSource = dsBudget;
                        csKeyContacts.GridRowStyleCSS = "normalrow";
                        csKeyContacts.GridHeaderRowCSS = "pl10 pr10 gridheader";
                        csKeyContacts.GridAlternatingRowCSS = "altrow";
                        csKeyContacts.ShowColumns = new int[] { 0, 1, 2, 3, 4 };
                        csKeyContacts.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                        csKeyContacts.GridWidth = Unit.Percentage(100);
                        csKeyContacts.GridAllowPaging = false;
                        csKeyContacts.BindGrid();
                        btnKeyCntsMoveRight.Enabled = false;
                        pnlKeyContact.Visible = false;
                    }
                    else
                    {
                        pnlKeyContact.Visible = true;
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnKeyCntsMoveRight_Click(object sender, EventArgs e)
        {
            try
            {
                foreach (GridViewRow gv in csKeyContacts.GridViewPaging.Rows)
                {
                    ImageButton selectButton = (ImageButton)gv.FindControl("imgRowSelect");
                    if (selectButton.AlternateText == "1")
                    {
                        BindAttachedKeyContacts(Convert.ToString(gv.Cells[6].Text), Convert.ToString(gv.Cells[1].Text), Convert.ToString(gv.Cells[2].Text));
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindAttachedKeyContacts(string KeyContactMId, string KeyContactSId, string strDesc)
        {
            try
            {
                if (ddlKeyContacts.SelectedIndex > -1)
                {
                    noteInfoPresenter = new NoteInfoPresenter(this);
                    using (DataSet dsBudget = noteInfoPresenter.GetKeyContactAttachment(NoteNumber, UnitNumber, KeyContactMId, KeyContactSId))
                    {
                        if (dsBudget.IsValidDataColumn())
                        {
                            if (strDesc != "")
                            {
                                if (dsBudget.Tables[0].Rows.Count > 0)
                                {
                                    if (dsBudget.Tables[0].Columns.Contains("Already"))
                                    {
                                        if (Convert.ToString(dsBudget.Tables[0].Rows[0]["Already"]).ToString().ToUpper() == "Already Exists".ToUpper())
                                        {
                                            string strMsg;
                                            strMsg = Convert.ToString(KeyContactSId) + " - " + Convert.ToString(strDesc) + " has already been added!";
                                            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('" + strMsg + "');", true);
                                            return;
                                        }

                                    }
                                    pnlKeyAttached.Visible = false;
                                }
                                else
                                {
                                    pnlKeyAttached.Visible = true;
                                }

                            }
                            csKeyContactAttached.GridClientID = "csKeyContactAttached";
                            csKeyContactAttached.DataSource = dsBudget;
                            csKeyContactAttached.GridRowStyleCSS = "normalrow";
                            csKeyContactAttached.GridHeaderRowCSS = "pl10 pr10 gridheader";
                            csKeyContactAttached.GridAlternatingRowCSS = "altrow";
                            csKeyContactAttached.ShowColumns = new int[] { 0, 1, 2, 3, 4 };
                            csKeyContactAttached.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                            csKeyContactAttached.GridWidth = Unit.Percentage(100);
                            csKeyContactAttached.GridAllowPaging = false;
                            csKeyContactAttached.BindGrid();
                            imgbtnDKeyContact.Visible = false;
                            if (csKeyContactAttached.GridViewPaging.Rows.Count == 0)
                                pnlKeyAttached.Visible = true;
                        }
                        else
                        {
                            pnlKeyAttached.Visible = false;
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void ddlKeyContacts_SelectedIndexChanged(object sender, EventArgs e)
        {
            try
            {
                if (ddlKeyContacts.SelectedIndex > -1)
                {
                    txtFindContact.Text = "";
                    BindKeyContacts();
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnFind_Click(object sender, EventArgs e)
        {
            try
            {
                BindKeyContacts();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void imgbtnDKeyContact_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRow in csKeyContactAttached.GridViewPaging.Rows)
                {
                    ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                    if (selectButton.AlternateText == "1")
                    {
                        noteInfoPresenter = new NoteInfoPresenter(this);
                        int intResult = noteInfoPresenter.DeleteKeyContactDelete(NoteNumber, UnitNumber, Convert.ToString(gvRow.Cells[1].Text));
                        BindAttachedKeyContacts("", "", "");
                        return;

                    }
                }
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Please select a Attached Key Contact to Delete?');", true);
                return;
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindNotePayRule()
        {
            try
            {

                this.ShowAll = chkPayoffShwAll.Checked ? "1" : "0";
                this.BorrowerNo = Convert.ToString(hdnBorrowerNo.Value);
                noteInfoPresenter = new NoteInfoPresenter(this);
                using (DataSet dsNoteRule = noteInfoPresenter.GetNotePayOffRules())
                {
                    if (TCLHelper.IsValidDataColumn(dsNoteRule))
                    {
                        using (DataSet dsNotePayOff = new DataSet())
                        {
                            dsNotePayOff.Tables.Add(dsNoteRule.Tables[0].Copy());
                            cgNotePayOffRules.GridClientID = "cgNotePayOffRules";
                            cgNotePayOffRules.DataSource = dsNotePayOff;
                            cgNotePayOffRules.GridRowStyleCSS = "normalrow";
                            cgNotePayOffRules.GridHeaderRowCSS = "pl10 pr10 gridheader";
                            cgNotePayOffRules.GridAlternatingRowCSS = "altrow";
                            cgNotePayOffRules.ShowColumns = new int[] { 1, 0, 2 };
                            cgNotePayOffRules.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Multiple;
                            cgNotePayOffRules.GridWidth = Unit.Percentage(100);
                            cgNotePayOffRules.GridAllowPaging = false;
                            cgNotePayOffRules.BindGrid();
                        }

                        if (dsNoteRule.Tables.Count > 1)
                        {
                            using (DataSet dsAttachedPayOff = new DataSet())
                            {
                                dsAttachedPayOff.Tables.Add(dsNoteRule.Tables[1].Copy());
                                BindNotePayOffAttach(dsAttachedPayOff);
                            }
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnPayoffMoveRight_Click(object sender, EventArgs e)
        {
            try
            {
                bool bFlag = false;
                tblNotePayOff.Visible = false;
                this.ShowAll = chkPayoffShwAll.Checked ? "1" : "0";
                this.BorrowerNo = Convert.ToString(hdnBorrowerNo.Value);
                noteInfoPresenter = new NoteInfoPresenter(this);
                StringBuilder strAttachError = new StringBuilder();

                foreach (GridViewRow gvRows in cgNotePayOffRules.GridViewPaging.Rows)
                {
                    CheckBox chkChecked = (CheckBox)gvRows.FindControl("chkMultipleSelect");
                    if (chkChecked.Checked)
                    {
                        bFlag = true;
                        this.RuleID = Convert.ToString(gvRows.Cells[1].Text);

                        string strError = string.Empty;
                        strError = "Loan Number: " + this.NoteNumber + " " + this.UnitNumber + "\\r\\n \\r\\n Rule: " + Convert.ToString(gvRows.Cells[1].Text) + "\\r\\n         " + Convert.ToString(gvRows.Cells[3].Text + "\\r\\n \\r\\n");

                        using (DataSet dsPayOff = noteInfoPresenter.GetNotePayOffRulesById())
                        {
                            if (dsPayOff.Tables.Count > 0 || dsPayOff != null)
                            {
                                if (dsPayOff.Tables[0].Rows.Count > 0)
                                {
                                    DataView dvPayOff = (DataView)dsPayOff.Tables[0].DefaultView;
                                    dvPayOff.RowFilter = "RULEID = '" + Convert.ToString(gvRows.Cells[1].Text) + "'";
                                    if (dvPayOff.Count == 0)
                                    {
                                        this.RuleType = Convert.ToString(gvRows.Cells[2].Text);
                                        this.RuleID = Convert.ToString(gvRows.Cells[1].Text);
                                        dvPayOff.RowFilter = "RULETYPE = '" + Convert.ToString(gvRows.Cells[2].Text) + "'";

                                        if (dvPayOff.Count == 0)
                                        {
                                            noteInfoPresenter.GetNotePayOffRules();
                                        }
                                        else
                                        {
                                            switch (Convert.ToString(gvRows.Cells[2].Text))
                                            {
                                                case "P":
                                                    // PRINC     MAX: 1, 1 or More Already
                                                    strAttachError.Append("alert('" + strError + "- Principal - Maximum rules per loan is 1.');");
                                                    break;
                                                case "F":
                                                    // FEE       MAX: 3
                                                    if (dvPayOff.Count >= 3)
                                                        strAttachError.Append("alert('" + strError + " - Fee - Maximum rules per loan is 3.');");
                                                    else
                                                        noteInfoPresenter.GetNotePayOffRules();
                                                    break;
                                                case "O":
                                                    // OTHER MAX: 2
                                                    if (dvPayOff.Count >= 2)
                                                        strAttachError.Append("alert('" + strError + " - Other - Maximum rules per loan is 2.');");
                                                    else
                                                        noteInfoPresenter.GetNotePayOffRules();
                                                    break;
                                                case "B":
                                                    // BB Col    MAX 1                   Col Rule Not Allowed @ NOTE Level
                                                    strAttachError.Append("alert('" + strError + " - Borrowing Base Collateral Rules Not Allowed At Note Level.');");
                                                    break;
                                                default:
                                                    noteInfoPresenter.GetNotePayOffRules();
                                                    break;
                                            }
                                        }
                                    }
                                    else
                                    {
                                        strAttachError.Append("alert('" + strError + " - Rule Already Attached');");
                                    }

                                }
                                else
                                {
                                    noteInfoPresenter.GetNotePayOffRules();
                                }
                            }
                        }
                    }

                }
                if (!bFlag)
                {
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('No Rule(s) selected to attach.');", true);
                }
                this.RuleID = "";
                BindNotePayRule();
                if (strAttachError.ToString().Trim() != "")
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", strAttachError.ToString(), true);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        private void BindNotePayOffAttach(DataSet dsNotePayOff)
        {
            try
            {
                cgNotPayOffRulsAttach.GridClientID = "cgNotPayOffRulsAttach";
                cgNotPayOffRulsAttach.DataSource = dsNotePayOff;
                cgNotPayOffRulsAttach.GridRowStyleCSS = "normalrow";
                cgNotPayOffRulsAttach.GridHeaderRowCSS = "pl10 pr10 gridheader";
                cgNotPayOffRulsAttach.GridAlternatingRowCSS = "altrow";
                cgNotPayOffRulsAttach.ShowColumns = new int[] { 1, 0, 2 };
                cgNotPayOffRulsAttach.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Multiple;
                cgNotPayOffRulsAttach.GridWidth = Unit.Percentage(100);
                cgNotPayOffRulsAttach.GridAllowPaging = false;
                cgNotPayOffRulsAttach.BindGrid();
                hdnNotePayOffCount.Value = Convert.ToString(dsNotePayOff.Tables[0].Rows.Count);
                if (TCLHelper.ConvertToBool(ViewState["NotePayOff"]))
                {
                    imgbtnNtPayoffRulsDelte.Enabled = false;
                    imgbtnNotePayOffEdit.Enabled = false;
                    if (TCLHelper.IsValidDataSet(dsNotePayOff))
                    {
                        if (dsNotePayOff.Tables[0].Rows.Count > 0)
                        {
                            imgbtnNtPayoffRulsDelte.Enabled = true;
                            imgbtnNotePayOffEdit.Enabled = true;
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void chkPayoffShwAll_Checked(object sender, EventArgs e)
        {
            BindNotePayRule();

        }

        protected void imgbtnNtPayoffRulsDelte_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRow in cgNotPayOffRulsAttach.GridViewPaging.Rows)
                {
                    CheckBox chkChecked = (CheckBox)gvRow.FindControl("chkMultipleSelect");
                    if (chkChecked.Checked)
                    {
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "DeleteNotePayOff('Are you sure you want to remove selected Payoff Rule(s)?');", true);
                        return;
                    }
                }
                if (TCLHelper.ConvertToInt(hdnNotePayOffCount.Value) > 0)
                {
                    //lblPayOffError.Text = "No Rule(s) selected to remove.";
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "alter", "alert('No Rule(s) selected to remove.');", true);
                    return;
                }
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnNotePayOff_Click(object sender, EventArgs e)
        {
            BindNotePayRule();
        }

        protected void btnNPODelete_Click(object sender, EventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRows in cgNotPayOffRulsAttach.GridViewPaging.Rows)
                {
                    CheckBox chkChecked = (CheckBox)gvRows.FindControl("chkMultipleSelect");
                    if (chkChecked.Checked)
                    {
                        this.IsDelete = "1";
                        RuleID = Convert.ToString(gvRows.Cells[1].Text);
                        RuleType = Convert.ToString(gvRows.Cells[2].Text);
                        noteInfoPresenter = new NoteInfoPresenter(this);
                        noteInfoPresenter.GetNotePayOffRules();
                    }

                }

                if (this.IsDelete == "1")
                {
                    tblNotePayOff.Visible = true;
                    trSuccess.Visible = true;
                    lblPayOffSuccess.Text = "Group ID deleted sucessfully";
                    lblPayOffSuccess.Visible = true;
                    trError.Visible = false;
                    lblPayOffError.Visible = false;
                    lblPayOffError.Text = string.Empty;
                }

                this.IsDelete = "0";
                this.RuleID = "";
                this.RuleType = "";
                BindNotePayRule();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }

        }

        protected void imgbtnEdit_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                foreach (GridViewRow gvRow in cgBudget.GridViewPaging.Rows)
                {
                    ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                    if (selectButton.AlternateText == "1")
                    {
                        sessionProvider.Set("BCLV1", Convert.ToString(gvRow.Cells[1].Text));
                        sessionProvider.Set("BdgGroupNote", Convert.ToString(gvRow.Cells[2].Text));
                        sessionProvider.Set("BdgtitleNote", Convert.ToString(ddlBudgets.SelectedItem.Text));
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "WBOpen();", true);
                        return;

                    }
                }


                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('Please select a row to edit');", true);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnEditBudget_Click(object sender, EventArgs e)
        {
            try
            {
                BindBudgetNotes(0);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnIPTemp_Click(object sender, EventArgs e)
        {
            try
            {
                GetIntrestProfileGrid();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnReleaseHide_Click(object sender, EventArgs e)
        {
            try
            {
                this.noteInfoPresenter.LoadRelsch();
                BindReleaseScheduleGrid(this.ListReleaseSchedule);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnEPTemp_Click(object sender, EventArgs e)
        {
            try
            {
                GetEquityProfileGrid();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnAddBudget_Click(object sender, EventArgs e)
        {
            try
            {
                noteInfoPresenter = new NoteInfoPresenter(this);
                bool IsExists;
                noteInfoPresenter.SaveBudget(NoteNumber, UnitNumber, Convert.ToString(ddlBudgets.SelectedValue), Convert.ToString(txtGroupID.Text), Convert.ToString(txtGroupDesc.Text), out IsExists);
                if (IsExists)
                {
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "confirm", "alert('Group ID already exists, cannot be added.');", true);
                    mpeAddBudget.Show();
                    BindBudgetNotes(0);
                    return;
                }

                tblMsgMPopup.Visible = false;
                BindBudgetNotes(0);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void imgbtnNotePayOffEdit_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                Int32 intMultiSelect = 0;
                string ruleId = string.Empty;
                foreach (GridViewRow gvRow in cgNotPayOffRulsAttach.GridViewPaging.Rows)
                {
                    CheckBox chkChecked = (CheckBox)gvRow.FindControl("chkMultipleSelect");
                    if (chkChecked.Checked)
                    {
                        intMultiSelect += 1;
                        ruleId = TCLHelper.RemoveHtmlWhiteSpace(gvRow.Cells[1].Text);
                    }
                }

                switch (intMultiSelect)
                {
                    case 0:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('Please select a row to edit.');", true);
                        break;
                    case 1:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Open", "wNotePayOffOpen('" + ruleId + "','1','NoteEdit');", true);
                        break;
                    default:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('Please select only ONE record to edit.');", true);
                        break;
                }

            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }

        protected void btnReleaseRules_Click(object sender, EventArgs e)
        {
            BindAttachedRuleGrid();
        }

        protected void imgbtnReleaseRule_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                Int32 intMultiSelect = 0;
                string ruleId = string.Empty;
                foreach (GridViewRow gvRow in cstGrdRlsPayoffAtchmnt.GridViewPaging.Rows)
                {
                    CheckBox chkChecked = (CheckBox)gvRow.FindControl("chkMultipleSelect");
                    if (chkChecked.Checked)
                    {
                        intMultiSelect += 1;
                        ruleId = TCLHelper.RemoveHtmlWhiteSpace(gvRow.Cells[2].Text);
                    }
                }

                switch (intMultiSelect)
                {
                    case 0:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('Please select a row to edit.');", true);
                        break;
                    case 1:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Open", "wNotePayOffOpen('" + ruleId + "','2','NoteEdit');", true);
                        break;
                    default:
                        ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "Alert", "alert('Please select only ONE record to edit.');", true);
                        break;
                }

            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }


        //protected void chkRevolving_CheckedChanged(object sender, EventArgs e)
        //{
        //    if (chkRevolving.Checked == true)
        //        chkFannieMae.Enabled = false;
        //    else
        //        chkFannieMae.Enabled = true;
        //}                      


        #endregion

        #region Sheeba(BorrowerBaseTerms)

        private void BindBBTerms()
        {
            noteInfoPresenter = new NoteInfoPresenter(this);
            using (DataSet dsBBTerms = noteInfoPresenter.GetBBTermsByNote())
            {
                if (dsBBTerms.IsValidDataSet())
                {
                    CstGrdBrwBaseTerms.DataSource = dsBBTerms;
                    //CstGrdBrwBaseTerms.TotalRecords = 1;
                    CstGrdBrwBaseTerms.GridAllowPaging = false;
                    CstGrdBrwBaseTerms.DataKeyNames = new string[] { "BBTermID", "Term ID" };
                    CstGrdBrwBaseTerms.HideColumns = new int[] { 7, 8, 9, 10, 11 };
                    //CstGrdBrwBaseTerms.ShowColumns = new int[] { 1, 2, 3, 5, 6, 10, 11 };
                    //CstGrdBrwBaseTerms.HideColumns = new int[] { 0, 1, 2 };
                    CstGrdBrwBaseTerms.AllowLinks = new int[] { 0 };//Term ID
                    CstGrdBrwBaseTerms.GridShowFooter = true;
                    CstGrdBrwBaseTerms.GridWidth = Unit.Percentage(100);
                    //CstGrdBrwBaseTerms.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                    CstGrdBrwBaseTerms.BindGrid();
                }
            }
        }

        protected void CstGrdBrwBaseTerms_OnGridRowEditing(object sender, EventArgs e)
        {
            GridViewRow gvr = ((TCL.Control.CustomGrid.ExtendGrid)(sender)).SelectedRow;
            //string strTermID = gvr.Cells[4].Text;//BBTermID
            string[] uniqueIds = CstGrdBrwBaseTerms.UniqueIDs;
            //Response.Redirect("NotesBB_terms.aspx?TermID=" + strTermID);
            ScriptManager.RegisterStartupScript(Page, Page.GetType(),
                       "Script", "WOpen('TEEdit','" + TCLHelper.GetData(uniqueIds[0]) + "@" +
                        TCLHelper.GetData(uniqueIds[1]) + "');", true);
        }

        #endregion

        #region VLU(DocTracking,Attachments,Dates)

        protected void imgbtnAtchmntsAdd_Click(object sender, ImageClickEventArgs e)
        {
            txtDocument.Text = string.Empty;
            mPopupAttachDoc.Show();
        }

        //protected void btnPrjctUseDfndfld_Click(object sender, EventArgs e)
        //{
        //    // Response.Redirect("UserDefinedFieldNoteInfo.aspx");
        //    string strNB = Convert.ToString(Request.QueryString["B"]);
        //    Response.Redirect("UserDefinedFieldNoteInfo.aspx?NB=" + strNB + "");
        //    //mdlpopupiframeuserdefined.Show();
        //}

        protected void lstbStndardArtchBrwDocTrack_SelectedIndexChanged(object sender, EventArgs e)
        {
            if (TCLHelper.GetData(ViewState["DocCheck"]).Equals(ModifyTrue, StringComparison.OrdinalIgnoreCase) == true)
            {
                if (lstbStndardArtchBrwDocTrack.Items.Count > 0)
                    btnDoctMove.Enabled = true;
                else
                    btnDoctMove.Enabled = false;
            }
            else
            {
                btnDoctMove.Enabled = false;
                btnDocRemove.Enabled = false;
                imgbtnDocTracAdd.Visible = false;
                imgbtnDocTracEdit.Visible = false;
            }
            //if (TCLHelper.GetData(ViewState["DocCheck"]).Equals(ModifyAttachTrue, StringComparison.OrdinalIgnoreCase) == true)
            //    btnDoctMove.Enabled = true;
            //else
            //    btnDoctMove.Enabled = false;
        }
        protected void lstbArtchBrwDocTrack_SelectedIndexChanged(object sender, EventArgs e)
        {
            if (TCLHelper.GetData(ViewState["DocCheck"]).Equals(ModifyTrue, StringComparison.OrdinalIgnoreCase) == true)
            {
                if (lstbArtchBrwDocTrack.Items.Count > 0)
                    btnDocRemove.Enabled = true;
                else
                    btnDocRemove.Enabled = false;
            }
            else
            {
                btnDoctMove.Enabled = false;
                btnDocRemove.Enabled = false;
                imgbtnDocTracAdd.Visible = false;
                imgbtnDocTracEdit.Visible = false;
                return;
            }
            string getDocid = lstbArtchBrwDocTrack.GetSelectedText();
            sessionProvider.Set("DOCTRACKDOCID", getDocid);
            string lenDocid = getDocid.Split('-')[0].ToString();
            btnDocRemove.Enabled = true;
            var docParameterName = "";

            if (lstbArtchBrwDocTrack.Items.Count > 0)
            {
                for (int i = 0; i < lstbArtchBrwDocTrack.Items.Count; i++)
                {
                    if (lstbArtchBrwDocTrack.Items[i].Selected)
                    {
                        ViewState.Add("DocId", Convert.ToString(lstbArtchBrwDocTrack.Items[i].Text));
                        if (docParameterName == "")
                            docParameterName = lstbArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                        else
                            docParameterName += "," + lstbArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                        hdnDocId.Value = docParameterName;
                        string strDesc = string.Empty;
                        if (string.IsNullOrEmpty(lstbArtchBrwDocTrack.Items[i].Text) == false)
                        {
                            if (lstbArtchBrwDocTrack.Items[i].Text.Split('-').Length > 0)
                                ViewState.Add("docdesc", Convert.ToString(lstbArtchBrwDocTrack.Items[i].Text.Split('-')[1]));
                        }
                    }
                }
            }
            if (!docParameterName.Trim().Contains(","))
            {
                if (lenDocid.Length > 3)
                {
                    imgbtnDocTracEdit.Visible = true;
                    imgbtnDocTracAdd.Visible = false;
                }
                else
                {
                    imgbtnDocTracEdit.Visible = false;
                    imgbtnDocTracAdd.Visible = true;
                }
            }
            else
            {
                imgbtnDocTracEdit.Visible = false;
                imgbtnDocTracAdd.Visible = false;
            }
        }

        protected void btnDoctMove_Click(object sender, EventArgs e)
        {
            var docParameterName = "";
            if (lstbStndardArtchBrwDocTrack.Items.Count > 0)
            {
                for (int i = 0; i < lstbStndardArtchBrwDocTrack.Items.Count; i++)
                {
                    if (lstbStndardArtchBrwDocTrack.Items[i].Selected)
                    {
                        if (docParameterName == "")
                            docParameterName = lstbStndardArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                        else
                            docParameterName += "," + lstbStndardArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                    }
                }
            }
            string vvDocId = docParameterName;
            DocID = vvDocId;
            this.noteInfoPresenter.InsertAttachments();
            this.noteInfoPresenter.LoadDocAttach();
            lstbArtchBrwDocTrack.DataBind();
            imgbtnDocTracAdd.Visible = false;
            imgbtnDocTracEdit.Visible = false;
        }

        protected void btnDocRemove_Click(object sender, EventArgs e)
        {
            var docDocIdName = "";
            if (lstbArtchBrwDocTrack.Items.Count > 0)
            {
                for (int i = 0; i < lstbArtchBrwDocTrack.Items.Count; i++)
                {
                    if (lstbArtchBrwDocTrack.Items[i].Selected)
                    {
                        if (docDocIdName == "")
                            docDocIdName = lstbArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                        else
                            docDocIdName += "," + lstbArtchBrwDocTrack.Items[i].Text.Split('-')[0].ToString();
                    }
                }
            }
            DocAttachSelected = docDocIdName;
            this.noteInfoPresenter.DeleteDoc();
            this.noteInfoPresenter.LoadDocAttach();
            lstbArtchBrwDocTrack.DataBind();
            imgbtnDocTracAdd.Visible = false;
            imgbtnDocTracEdit.Visible = false;
            if (lstbArtchBrwDocTrack.Items.Count == 0)
                btnDocRemove.Enabled = false;
        }

        protected void imgbtnAttachDetails_Click(object sender, ImageClickEventArgs e)
        {
            bool CheckAttach = true;
            foreach (GridViewRow gvRow in gvAttachments.GridViewPaging.Rows)
            {
                ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                if (selectButton.AlternateText == "1")
                {
                    CheckAttach = false;
                    string[] strAttached = ViewState["Attached"].ToString().Split(new char[] { '-' }, 2);
                    lblAttached.Text = strAttached[1] + " by " + strAttached[0];
                    lblNoteInfo.Text = NoteNumber + " " + UnitNumber;
                    lblAttachID.Text = ViewState["AttachID"].ToString();
                    lblDescription.Text = ViewState["Description"].ToString();
                    //lblFileLocation.Text = ViewState["FileLoc"].ToString();
                    mPopupAttachdetails.Show();
                }
            }
            if (CheckAttach)
                ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('Please select a record to Details.');", true);

        }

        protected void btnAttachmentOk_Click(object sender, EventArgs e)
        {
            if (this.fuAttachments.HasFile)
            {
                InsertAttachment();
            }
        }

        private void InsertAttachment()
        {
            noteInfoPresenter = new NoteInfoPresenter(this);
            AttachmentEntity attachmentEntity = new AttachmentEntity();
            double AttachmentID = noteInfoPresenter.GetRandomId();
            Stream strm = this.fuAttachments.PostedFile.InputStream;
            BinaryReader br = new BinaryReader(strm);
            Byte[] size = br.ReadBytes((int)strm.Length);
            attachmentEntity.AttachedTo = "N";
            attachmentEntity.AttachmentID = AttachmentID;
            attachmentEntity.BNUMBER = string.Empty; ;
            attachmentEntity.CreatedBy = Session["User"].ToString().ToUpper();
            attachmentEntity.CreatedDate = DateTime.Now.ToLocalTime();
            attachmentEntity.FileDescription = txtDocument.Text;
            if (attachmentEntity.FileDescription == string.Empty)
                attachmentEntity.FileDescription = this.fuAttachments.FileName;
            attachmentEntity.OriginalFilename = Path.GetFullPath(fuAttachments.PostedFile.FileName);  //this.fuAttachments.FileName; 
            attachmentEntity.PhysicalDocument = size;
            attachmentEntity.PNOTENO = NoteNumber;
            attachmentEntity.PUNIT = UnitNumber;
            attachmentEntity.UNCFlag = 0;
            noteInfoPresenter.InsertAttachments(attachmentEntity);
            //   if(gvAttachments.RowsPerPage!=null)
            // ARowsPerPage = gvAttachments.RowsPerPage;
            //APageNumber = 1;
            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('New record successfully added.');", true);
            BindBorrowerAttachments();
        }

        private void BindBorrowerAttachments()
        {
            // from  
            Int64 TotalRowCount = 0;
            noteInfoPresenter = new NoteInfoPresenter(this);
            imgbtnAtchmntsDel.Visible = false;
            imgbtnAttachDetails.Visible = false;
            using (DataSet dsBorrowerAttachments = noteInfoPresenter.GetBorrowerAttachments(out TotalRowCount, "N", NoteNumber, UnitNumber, iRowsPerPage, iPageNumber))
            {
                if (dsBorrowerAttachments.IsValidDataColumn())
                {

                    if (TCLHelper.ConvertToBool(ViewState["ModifyAttach"]))
                    {
                        imgbtnAtchmntsAdd.Visible = true;
                        if (TotalRowCount > 0)
                        {
                            imgbtnAtchmntsDel.Enabled = true;
                            imgbtnAtchmntsDel.Visible = true;
                        }
                    }

                    if (TotalRowCount > 0)
                    {
                        imgbtnAttachDetails.Visible = true;
                        imgbtnAttachDetails.Enabled = true;
                    }

                    gvAttachments.GridRowStyleCSS = "normalrow";
                    gvAttachments.GridHeaderRowCSS = "pl10 pr10 gridheader";
                    gvAttachments.GridAlternatingRowCSS = "altrow";
                    gvAttachments.TotalRecords = TotalRowCount;
                    gvAttachments.AllowLinks = new int[] { 0 };
                    gvAttachments.HideColumns = new int[] { 2, 3, 4 };
                    gvAttachments.DataKeyNames = new string[] { "Description" };
                    gvAttachments.GridAllowPaging = true;
                    gvAttachments.DeleteMode = Control.CustomGrid.ExtendGrid.Deletemode.Single;
                    gvAttachments.RowsPerPage = iRowsPerPage;
                    gvAttachments.PageNumber = iPageNumber;
                    gvAttachments.DataSource = dsBorrowerAttachments;
                    gvAttachments.BindGrid();
                }
            }
        }

        protected void gvAttachments_GridCheckedChange(object sender, ImageClickEventArgs e)
        {
            GridViewRow gvRow = gvAttachments.SelectedRow;
            LinkButton lnkButton = (LinkButton)gvRow.FindControl("lnk0");
            ViewState["Description"] = Convert.ToString(lnkButton.Text);
            ViewState["Attached"] = gvRow.Cells[2].Text;
            ViewState["AttachID"] = gvRow.Cells[3].Text;
            ViewState["FileLoc"] = gvRow.Cells[4].Text;

        }

        protected void gvAttachments_GridRowEditing(object sender, EventArgs e)
        {
            GridViewRow gvRow = gvAttachments.SelectedRow;
            LinkButton lnkAttach = (LinkButton)gvRow.FindControl("lnk0");
            string createdDate = gvRow.Cells[2].Text.ToString();
            DataTable dt = new DataTable();
            dt = noteInfoPresenter.GetDetails(createdDate);
            if (dt != null)
            {
                string strUri = "ViewDocs.aspx?DocId=" + Convert.ToString(gvRow.Cells[3].Text);
                ScriptManager.RegisterStartupScript(Page, Page.GetType(), "Script", "javascript:window.open('" + strUri + "');", true);
            }
        }

        protected void gvAttachments_GridRowCreated(object sender, GridViewRowEventArgs e)
        {
            if (e.Row.RowType == DataControlRowType.DataRow)
            {
                LinkButton linkAttach = (LinkButton)e.Row.FindControl("lnk0");
                ToolkitScriptManager1.RegisterPostBackControl(linkAttach);
            }
        }

        protected void imgbtnAtchmntsDel_Click(object sender, ImageClickEventArgs e)
        {
            try
            {
                try
                {
                    foreach (GridViewRow gvRow in gvAttachments.GridViewPaging.Rows)
                    {
                        ImageButton selectButton = (ImageButton)gvRow.FindControl("imgRowSelect");
                        if (selectButton.AlternateText == "1")
                        {
                            noteInfoPresenter = new NoteInfoPresenter(this);
                            noteInfoPresenter.DeleteDocAttachment(this.NoteNumber, this.UnitNumber, Convert.ToString(gvRow.Cells[3].Text));
                            BindBorrowerAttachments();
                            ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('Attachment deleted successfully.');", true);
                            return;

                        }
                    }
                    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('Please select a record to delete.');", true);
                }
                catch (Exception ex)
                {
                    Logger.LogException(ex, Level.Error);
                }

                //int istatus = 0;
                //gvAttachments


                //if (ViewState["Attached"] == null)
                //{
                //    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('Please select a record to delete.');", true);
                //    // lblErrorFail.Text = "Please select a record to delete.";
                //}
                //else
                //{
                //    istatus = noteInfoPresenter.DeleteAttachment("N", ViewState["Attached"].ToString());
                //    //lblErrorSuccess.Text = "Code deleted successfully.";
                //    ScriptManager.RegisterStartupScript(upanel, upanel.GetType(), "msg", "alert('Code deleted successfully.');", true);
                //}
                //BindBorrowerAttachments();
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);
            }
        }


        #endregion

        #region Save NoteInfo


        protected void btnProjectCancel_Click(object sender, EventArgs e)
        {
            if (hdnInquiry.Value == "Inquiry")
            { Response.Redirect("InquiryBorrower.aspx"); }
            else
            { Response.Redirect("Notes.aspx"); }


        }

        protected void btnSave_Click(object sender, EventArgs e)
        {
            InvokeJavascriptFunction("Save1('" + this.mProp_Inquiry + "','" + this.txt_Adminstratorflag + "','" + this.Action + "','" + this.bRenewal + "','" + this.NoteMode + "','" + this.nRenewalCount + "','" + this.dPrevMatDate + "','" + this.dPrvCompDate + "')");
        }

        protected void btnSaveProcess_Click(object sender, EventArgs e)
        {
            try
            {
                string eventTarget = this.Request.Form["__EVENTTARGET"];
                string eventArg = this.Request.Form["__EVENTARGUMENT"];
                string sMsg = string.Empty;
                string effDate = string.Empty;
                string oldEffDate = string.Empty;
                int bRateChange;
                long nMonths;
                if (eventArg.Equals("save1", StringComparison.OrdinalIgnoreCase))
                {
                    Dictionary<string, string> dictScriptValues = TCLHelper.JavascriptDeSerializer<Dictionary<string, string>>(eventTarget);
                    this.bFeePostCompDate = TCLHelper.ConvertToInt(dictScriptValues["bFeePostCompDate"]);
                    this.bFeePostMaturity = TCLHelper.ConvertToInt(dictScriptValues["bFeePostMaturity"]);
                    ViewState.Add("bFeePostCompDate", this.bFeePostCompDate);
                    ViewState.Add("bFeePostMaturity", this.bFeePostMaturity);
                    if (this.UnitNumber != "000" && this.NoteType != "B")
                    {
                        CalcAllocCommit();
                        this.cAlloc = TCLHelper.ConvertToDouble(TCLHelper.ConvertFromUSCurrency(txtTotalAllocated.Text));
                        ViewState.Add("cAlloc", this.cAlloc);
                        this.cEst = TCLHelper.ConvertToDouble(TCLHelper.ConvertFromUSCurrency(txtTotalEstimated.Text));
                        ViewState.Add("cEst", this.cEst);
                        if (this.cEst != this.cAlloc)
                        {
                            this.cDiff = this.cEst - this.cAlloc;
                            ViewState.Add("cDiff", this.cDiff);
                        }
                        InvokeJavascriptFunction("Save2('" + cEst + "','" + cAlloc + "');");
                        return;
                    }
                    else
                    {
                        InvokeJavascriptFunction("Save3('" + TCLHelper.ConvertFromUSCurrency(this.txtFincTabprincBal3.Text) + "','" + TCLHelper.ConvertFromUSCurrency(this.txtFincTabLoanCommit3.Text) + "');");
                        return;
                    }
                }
                if (eventArg.Equals("save2", StringComparison.OrdinalIgnoreCase))
                {
                    InvokeJavascriptFunction("Save3('" + TCLHelper.ConvertFromUSCurrency(this.txtFincTabprincBal3.Text) + "','" + TCLHelper.ConvertFromUSCurrency(this.txtFincTabLoanCommit3.Text) + "');");
                    return;
                }
                if (eventArg.Equals("save3", StringComparison.OrdinalIgnoreCase))
                {
                    if (this.noteInfoPresenter.ComRuleValidate() == false)
                    {
                        //TabNoteInfo.ActiveTab = TabNoteInfo.Tabs[5];
                        //TabNoteInfo.Tabs[5].Focus();
                        //return;
                    }

                    if (this.noteInfoPresenter.RuleChangedCommitmentAmt() == false)
                    {
                        // TabNoteInfo.ActiveTab = TabNoteInfo.Tabs[5];
                        // TabNoteInfo.Tabs[5].Focus();
                        //return;
                    }

                    if (this.Action == 1)
                    {
                        bRateChange = Convert.ToInt32(false);
                        DataSet dsRate = null;
                        bool isDateRange = false;
                        DateTime? toDate = DateTime.Now;
                        dsRate = this.noteInfoPresenter.CmdCommand(TCLHelper.ConvertToDateTimeNullable(txtFincTabEffctDate1.Text), toDate, out isDateRange);
                        if (isDateRange == true)
                        {
                            sMsg = "Interest rate changes have occurred between the commitment effective date and the current date.";
                            sMsg = sMsg + "You should enter an interest profile for each interest rate effective date ";
                            sMsg = sMsg + "or the interest will be calculated to date using only the current rate.";
                            sMsg = sMsg + "Continue with save?";
                            InvokeJavascriptFunction("Save4('" + sMsg + "')");
                            return;
                        }

                        dsRate = this.noteInfoPresenter.CmdCommandValidate(TCLHelper.ConvertToDateTimeNullable(txtFincTabEffctDate1.Text), toDate, out isDateRange);
                        //till sp -uspCmdCommandValidate

                        if (isDateRange == true)
                        {
                            sMsg = "Interest rate changes have ocurred between the Equity Profile's effective date and the current date.  ";
                            sMsg = sMsg + "You will need to create an Equity Interest Profile for each rate change effective date.  ";
                            sMsg = sMsg + "Continue with save?";
                            InvokeJavascriptFunction("Save5('" + sMsg + "')");
                            return;
                        }
                        //till sp -uspCmdCommand
                    }
                }
                if (eventArg.Equals("save4", StringComparison.OrdinalIgnoreCase))
                {
                    bool isDateRange = false;
                    bRateChange = 0;
                    DataSet dsRate1 = new DataSet();
                    DateTime? toDate = DateTime.Now;
                    dsRate1 = this.noteInfoPresenter.CmdCommandValidate(TCLHelper.ConvertToDateTimeNullable(txtFincTabEffctDate1.Text), toDate, out isDateRange);
                    //till sp -uspCmdCommandValidate

                    if (bRateChange != 0)
                    {
                        sMsg = "Interest rate changes have ocurred between the Equity Profile's effective date and the current date.  ";
                        sMsg = sMsg + "You will need to create an Equity Interest Profile for each rate change effective date.  ";
                        sMsg = sMsg + "Continue with save?";
                        InvokeJavascriptFunction("Save5('" + sMsg + "')");
                        return;
                    }
                }

                if (eventArg.Equals("save5", StringComparison.OrdinalIgnoreCase) || eventArg.Equals("save3", StringComparison.OrdinalIgnoreCase) || eventArg.Equals("save4", StringComparison.OrdinalIgnoreCase))
                {
                    //                ' 8.11.0 - RFC 15151
                    //        With mobjAdministrators
                    //            If .NotFound Then                                   ' Initial Value NOT Found; INVALID
                    //                If Trim$(UCase$(cboNote(18))) = Trim$(UCase$(.InitalValue)) Then  ' Still Same
                    //                    MsgBox "Current 'Administrator' is not Valid, Please select a valid user"
                    //                    tbNoteInfo.ActiveTab = GetTabIndex("PROJECT")
                    //                    GoTo SetNoteBailOut
                    //                End If
                    //            End If
                    //        End With
                    //' 8.11.0 - RFC 15151
                    this.bFeePostCompDate = TCLHelper.ConvertToInt(ViewState["bFeePostCompDate"]);
                    if (bFeePostCompDate != 0)
                    {
                        nMonths = TCLHelper.DateDiff("M", DateTime.Parse(this.dPrvCompDate), txtDateTabCnsCmpl.Text);
                        //mGoSubStack.PutPosition(1); 
                        double nFeeAmt;
                        bool blnPostExtFee = true;
                        DataSet dsAmountDetail = this.noteInfoPresenter.CalcAmtValidate(this.BorrowerNo, this.NoteNumber, this.UnitNumber, nMonths, out nFeeAmt, out blnPostExtFee);
                        this.nFeeAmount = nFeeAmt;

                        InvokeJavascriptFunction("Save7('" + this.blnPostExtFee + "','" + nFeeAmount + "','" + bFeePostCompDate + "','');");
                        return;
                        //if (this.blnPostExtFee == false)
                        //{
                        //    //MessageBox.Show("Extension fee cannot be calculated.  The loan is not participated or the participant interest profile is missing.", null, vbOKOnly, vbOKOnly);
                        //    goto Continue;
                        //}

                        //if (this.nFeeAmount <= 0)
                        //{
                        //    //MessageBox.Show("No Extension Fee Required.", null, vbOKOnly, vbOKOnly);
                        //    goto Continue;
                        //}
                        //PostFee(this.NoteNumber, this.UnitNumber, cboNote[0], "NI:Extension", nMonths, nFeeAmount, "Extension Fee", true);
                    }
                    else
                    {
                        this.bFeePostMaturity = TCLHelper.ConvertToInt(ViewState["bFeePostMaturity"]);
                        int isValidProp = 0;
                        if (this.NoteType == "M")
                        {
                            if (txtDateTabQotPost.Text != string.Empty)
                            {
                                DataSet dsPropVal = this.noteInfoPresenter.GetValidateProperty();
                                if (dsPropVal.IsValidDataSet())
                                {
                                    isValidProp = -1;
                                }
                            }
                        }

                        InvokeJavascriptFunction("Save7('" + this.blnPostExtFee + "','" + nFeeAmount + "','" + bFeePostCompDate + "','" + bFeePostMaturity + "','" + isValidProp + "','" + this.NoteType + "');");
                        return;
                    }
                }

                if (eventArg.Equals("save7", StringComparison.OrdinalIgnoreCase) || eventArg.Equals("save3", StringComparison.OrdinalIgnoreCase))
                {
                    if (chkNonAccural.Checked != this.mnPrvNonAccrual)
                    {
                        InvokeJavascriptFunction("LoadNonAccural()");
                        return;
                    }

                    goto Continue;
                }

                if (eventArg.Equals("savefinal", StringComparison.OrdinalIgnoreCase) || eventArg.Equals("save3", StringComparison.OrdinalIgnoreCase))
                {
                    effDate = eventTarget.Split(',')[0].Split(':')[1];
                    oldEffDate = eventTarget.Split(',')[1].Split(':')[1];
                    goto Continue;
                }

                if (eventArg.Equals("auditresponse", StringComparison.OrdinalIgnoreCase))
                {
                    Response.Redirect("Notes.aspx");
                }

            Continue:
                //if (bFeePostMaturity != 0)
                //{
                //    //PostFee(this.NoteNumber, this.UnitNumber, cboNote[0], "NI:Renewal", , , "Renewal Fee", true);
                //}

                //if (ddlMLoc.SelectedIndex > 0)
                //{
                //    if (ddlSLoc.SelectedIndex == 0)
                //    {
                //        //MessageBox.Show("If a Master LOC is selected then a Sub LOC must be selected.", "Master/Sub Line of Credit", vbOKOnly + vbInformation, vbOKOnly + vbInformation);
                //        return;
                //    }
                //}
                //else
                //{
                //    if (ddlSLoc.SelectedIndex > 0)
                //    {
                //        //MessageBox.Show("If a Sub LOC is selected then a Master LOC must be selected.", "Master/Sub Line of Credit", vbOKOnly + vbInformation, vbOKOnly + vbInformation);
                //        return;
                //    }
                //}

                //if (this.mblnLOCProblemOnLoad)
                //{
                //    if (ddlMLoc.SelectedIndex <= 0)
                //    {
                //        sMsg = "While Loading this notes information, the Master/Sub LOC originally assigned could not be located" + "\n" + "\n";
                //        sMsg = sMsg + "A Line of Credit has not been set for this loan and the assignemt will be removed if you save now" + "\n" + "\n";
                //        sMsg = sMsg + "Press YES to continue, NO to modify.";
                //        //if (MessageBox.Show(sMsg, "Problem with Line of Credit", vbCritical + vbYesNo, vbCritical + vbYesNo) == vbNo)
                //        //{
                //        //    return;
                //        //}
                //    }
                //    else
                //    {
                //    }
                //}

                //if (this.NoteType == "M")
                //{
                //    if (txtDateTabQotPost.Text != string.Empty)
                //    {
                //        sSql = "Select * from Property Where PNoteno = '" + this.NoteNumber + "' and PUnit <> '000' and PPDate is null";
                //        DataSet rsMasterSubPayoff = null;
                //        rsMasterSubPayoff = this.noteInfoPresenter.uspGetValidateProperty();
                //        if (rsMasterSubPayoff.IsValidDataSet())
                //        {
                //            //MessageBox.Show("There are Sub Notes attached to this Master Note which are not paid-off. You cannot input a Payoff Posted date until all Sub Notes are paid-off.", "Master\\Sub Note Payoff", vbOKOnly + vbInformation, vbOKOnly + vbInformation);
                //            //tbNoteInfo.ActiveTab = 2;
                //            txtDateTabQotPost.Focus();
                //            return;
                //        }
                //    }
                //}

                //till sp - ??????????????????????????????
                Dictionary<string, string> novinputParams = new Dictionary<string, string>();
                novinputParams.Add("PNOTE", this.NoteNumber);
                novinputParams.Add("PUNIT", this.UnitNumber);
                novinputParams.Add("ExitState", "YES");
                novinputParams.Add("EffDate", oldEffDate);
                novinputParams.Add("GLTable", string.Empty);
                novinputParams.Add("TranDate", DateTime.Now.ToString());
                novinputParams.Add("PNUMBER", this.BorrowerNo);
                novinputParams.Add("TYPE", string.Empty);
                novinputParams.Add("ICODE", string.Empty);
                novinputParams.Add("TRANCODE", string.Empty);
                novinputParams.Add("strUser", this.UserName);
                novinputParams.Add("EventSource", "NA");
                novinputParams.Add("BilledAdj", "0");
                novinputParams.Add("BookedAdj", "0");
                novinputParams.Add("UnbookedAdj", "0");
                novinputParams.Add("RecID", new CommonService("ACC04").RecordID().ToString());
                novinputParams.Add("EventType", "N");
                novinputParams.Add("blnNoGLImpact", "false");
                novinputParams.Add("bln_DailyAccrual", string.Empty);
                novinputParams.Add("blnNonAccrual", chkNonAccural.Checked.ToString());
                novinputParams.Add("SYSDATE", effDate);
                novinputParams.Add("Flag", string.Empty);
                //call nonaccural window.
                this.noteInfoPresenter.NonAccrualValidate(novinputParams);
                SaveNote();
                this.noteInfoPresenter.ShowMessageBox("Saved Successfully.");
                if (this.blnAUDITRPT == true)
                {
                    InvokeAuditReport();
                    return;
                }
                Response.Redirect("Notes.aspx");
            }
            catch (Exception ex)
            {

            }
        }

        private void InvokeAuditReport()
        {
            //calling sp
            string sMsg = string.Empty;
            bool bTax = false;
            bool bLOCMDate = false;
            bool bLOC = false;
            bool bLOCTerms = false;
            bool bLOCParentTotal = false;
            bool bLegalDesc = false;
            bool bIntProf = false;
            bool bBillOpt = false;
            bool bNLEqtProf = false;
            bool bBLEqtProf = false;
            string sMsgSubLMDate = string.Empty;
            string sMsgMasterLMDate = string.Empty;
            string sMsgLOC = string.Empty;
            string strBudget = string.Empty;
            bool blnShowReport = false;
            bool blnBorrowingBase = false;
            int nRow = 0;
            int cExceed = 0;
            int mcurParentTotalExceed = 0;
            string mstrTermsMsg = string.Empty;
            DataSet ds = null;

            if (this.NoteType == "B")
                blnBorrowingBase = true;

            if (this.blnAR_TAXID == true || this.blnAR_LDESC || this.blnAR_LOC || this.blnAR_LOCMAT || this.blnAR_INT || this.blnAR_BILLOPT || this.blnAR_BUD || this.blnAR_BUDPROF || this.blnAR_EQTPROF || this.blnAR_LOCPARENTTOTAL || this.blnAR_LOCTERMS)
            {
                Dictionary<string, string> dictAuditParams = new Dictionary<string, string>();
                dictAuditParams.Add("gsNoteType", this.NoteMode);
                dictAuditParams.Add("PNOTENO", this.NoteNumber);
                dictAuditParams.Add("PUNIT", this.UnitNumber);
                dictAuditParams.Add("bln_AR_TAXID", Convert.ToString(this.blnAR_TAXID));
                dictAuditParams.Add("bln_AR_LDESC", Convert.ToString(this.blnAR_LDESC));
                dictAuditParams.Add("bln_AR_LOC", Convert.ToString(this.blnAR_LOC));
                dictAuditParams.Add("bln_AR_LOCMAT", Convert.ToString(this.blnAR_LOCMAT));
                dictAuditParams.Add("bln_AR_INT", Convert.ToString(this.blnAR_INT));
                dictAuditParams.Add("bln_AR_BILLOPT", Convert.ToString(this.blnAR_BILLOPT));
                dictAuditParams.Add("bln_AR_BUD", Convert.ToString(this.blnAR_BUD));
                dictAuditParams.Add("bln_AR_BUDPROF", Convert.ToString(this.blnAR_BUDPROF));
                dictAuditParams.Add("bln_AR_EQTPROF", Convert.ToString(this.blnAR_EQTPROF));
                dictAuditParams.Add("bln_AR_LOCPARENTTOTAL", Convert.ToString(this.blnAR_LOCPARENTTOTAL));
                dictAuditParams.Add("bln_AR_LOCTERMS", Convert.ToString(this.blnAR_LOCTERMS));

                dictAuditParams.Add("cboNote13", ddlArea.SelectedValue);
                dictAuditParams.Add("cboNote14", ddlLocal.SelectedValue);
                dictAuditParams.Add("cboNote15", ddlMClass.SelectedValue);
                dictAuditParams.Add("cboNote16", ddlSClass.SelectedValue);
                dictAuditParams.Add("cboNote2", drpdwnlstState.SelectedValue);
                dictAuditParams.Add("cboNote4", ddlStatus.SelectedValue);
                using (DataSet dsAudit = this.noteInfoPresenter.GetAuditInfo(dictAuditParams))
                {

                    if (dsAudit.IsValidDataSet())
                    {
                        bTax = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bTax"]));
                        bLOCMDate = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bLOCMDate"]));
                        bLOC = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bLOC"]));
                        bLegalDesc = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bLegalDesc"]));
                        bIntProf = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bIntProf"]));
                        bBillOpt = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bBillOpt"]));
                        bNLEqtProf = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bNLEqtProf"]));
                        bBLEqtProf = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bBLEqtProf"]));
                        sMsgSubLMDate = TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["sMsgSubLMDate"]);
                        sMsgMasterLMDate = TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["sMsgMasterLMDate"]);
                        sMsgLOC = TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["sMsgLOC"]);
                        bLOCTerms = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bLOCTerms"]));
                        bLOCParentTotal = TCLHelper.ConvertToBool(TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["bLOCParentTotal"]));
                        mstrTermsMsg = TCLHelper.GetData(dsAudit.Tables[0].Rows[0]["mstrTermsMsg"]);
                    }
                }
            }
            else
            {
                ScriptManager.RegisterStartupScript(Page, this.GetType(), "alert", "javascript:alert('No Audit Report options have been selected in the System Profile. Cannot perform Audit report.'", true);
                goto ExitAuditReport;
            }

            if (bTax)
            {
                sMsg = "Borrower TaxID is missing" + "^";
                blnShowReport = true;
            }
            if (bLOCMDate)
            {
                sMsg = sMsg + sMsgMasterLMDate + "^";
                blnShowReport = true;
            }
            if (bLOCMDate)
            {
                sMsg = sMsgSubLMDate + "^";
                blnShowReport = true;
            }
            if (bLOC)
            {
                sMsg = sMsg + "Sub Line of Credit Commitment exceeded by " + (cExceed).ToString("Currency") + "^";
                blnShowReport = true;
            }
            if (bLOCParentTotal)
            {
                sMsg = sMsg + "The sum of all Master Commitments, including Child records, exceed the Parent Total Line by " + (mcurParentTotalExceed).ToString("Currency") + "^";
            }
            if (bLOCTerms)
            {
                if (string.IsNullOrEmpty(mstrTermsMsg.Trim()) == false)
                {
                    sMsg = sMsg + mstrTermsMsg + "^";
                    blnShowReport = true;
                }
                if (mstrExceedSUBLOC != "")
                {
                    sMsg = sMsg + mstrExceedSUBLOC + "^";
                    blnShowReport = true;
                }
            }
            if (bLegalDesc && !blnBorrowingBase)
            {
                sMsg = sMsg + "Legal Description is missing" + "^";
                blnShowReport = true;
            }
            if (this.blnAR_BUD && ((this.cAlloc - this.cEst) != 0) && blnBorrowingBase == false)
            {
                sMsg = sMsg + "Budget Estimated " + TCLHelper.ConvertToUSCurrency(this.cEst) + " - Allocated " + TCLHelper.ConvertToUSCurrency(this.cAlloc) + "  =  " + TCLHelper.ConvertToUSCurrency(this.cDiff) + "^";
                blnShowReport = true;
            }
            if (bIntProf)
            {
                if (TCLHelper.Trim(sMsgLOC) == "")
                {
                    sMsg = sMsg + "Interest Profile or Interest Rate missing" + "^";
                }
                else
                {
                    sMsg = sMsg + sMsgLOC + "^";
                }
                blnShowReport = true;
            }
            if (bBillOpt)
            {
                if (string.IsNullOrEmpty(sMsgLOC) == true)
                {
                    sMsg = sMsg + "Interest Profile or Billing Cycle missing" + "^";
                }
                else
                {
                    sMsg = sMsg + sMsgLOC + "^";
                }
                blnShowReport = true;
            }
            if (bNLEqtProf)
            {
                sMsg = sMsg + "Note Level Equity Interest Profile missing or rate not found." + "^";
                blnShowReport = true;
            }

            if (bBLEqtProf)
            {
                ds = this.noteInfoPresenter.NoteEqtyProfGet();
                if (ds.IsValidDataSet())
                {
                    for (int i = 0; i < ds.Tables[0].Rows.Count; i++)
                    {
                        sMsg = sMsg + TCLHelper.GetData(ds.Tables[0].Rows[i]["ErrMsg"]) + "^";
                    }
                }
            }

            if (blnShowReport)
            {
                ScriptManager.RegisterStartupScript(Page, Page.GetType(), "Script", "WOpenAuditTrail('" + this.NoteNumber + "','" + this.UnitNumber + "' ,'" + sMsg + "');", true);
            }
        ExitAuditReport:
            return;
        }

        private void InvokeJavascriptFunction(string functionName)
        {
            ScriptManager.RegisterStartupScript(this, this.GetType(), "InVokeFunc", functionName, true);
        }

        public void CalcAllocCommit()
        {
            DataSet dsCalculate = this.noteInfoPresenter.CalcAllocCommit();
            bool mblnGenDrawBudget = false;

            if (dsCalculate.IsValidDataSet() == true)
            {
                foreach (DataRow drow in dsCalculate.Tables[0].Rows)
                {
                    txtAlctCommit.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtAlctCommit.Text) + (TCLHelper.ConvertToDouble(drow["BCCOST"]) - TCLHelper.ConvertToDouble(drow["BCEQUITY"])));
                    txtTotalAllocated.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtTotalAllocated.Text) + TCLHelper.ConvertToDouble(drow["BCCOST"]));
                }
            }
            else
            {
                DataSet adoBudget = this.noteInfoPresenter.GetBudget();
                if (adoBudget.IsValidDataSet())
                {
                    foreach (DataRow drow in adoBudget.Tables[0].Rows)
                    {
                        if ((TCLHelper.GetData(drow["BCID"]) + TCLHelper.GetData(drow["BCLV1"]) + TCLHelper.GetData(drow["BCLV2"])) == "9999900")
                        {
                            txtAlctCommit.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtAlctCommit.Text) + TCLHelper.ConvertToDouble(txtFincTabConstRslt.Text));
                            mblnGenDrawBudget = true;
                            txtTotalAllocated.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtTotalAllocated.Text) + TCLHelper.ConvertToDouble(txtFincTabConstRslt.Text));
                        }
                    }
                }
            }

            txtAlctCommit.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtAlctCommit.Text));
            txtTotalAllocated.Text = TCLHelper.ConvertToUSCurrency(TCLHelper.ConvertToDouble(txtTotalAllocated.Text));
        }

        public void SaveNote()
        {
            //blnLOCSEQ = false;
            //if (!Status_Begin("Saving All Note Information", "Selecting Note Record", 0, 5, false)) 
            //{
            //}
            //if (!Status_Refresh(1, "Saving Note Information")) {
            //}

            string sSql = string.Empty;
            ////if (chkNote[0].Tag==true)
            ////{
            //    //mGoSubStack.PutPosition(1); 
            //            //goto AddToSQLStmt; 
            //            //GoSubReturnPosition1:
            //    sSql = sSql+"PPTYPE = '"+(chkNote[0].Checked==false ? "N" : "Y")+"'";
            ////}

            //if (chkNote[1].Tag==true) 
            //{
            //if (chkNote[1].Checked!=Math.Abs(mnPrvNonAccrual)) 
            //{
            //    mGoSubStack.PutPosition(2); goto AddToSQLStmt; GoSubReturnPosition2:
            //    sSql = sSql+"PNOACCRUAL = "+(chkNote[1].Checked==false ? 0 : -1); // Field Can't Take Boolean Values
            //}
            //}

            //if (chkNote[2].Tag==true) {
            //if (chkNote[2].Checked!=Math.Abs(mnPrvInDefault)) {
            //mGoSubStack.PutPosition(3); goto AddToSQLStmt; GoSubReturnPosition3:
            //sSql = sSql+"PINDEFAULT = "+(chkNote[2].Checked==false ? 0 : -1); // Field Can't Take Boolean Values
            //}
            //}
            //if (chkNote[3].Tag==true) {
            //if (chkNote[3].Checked!=Math.Abs(mnPrvStopFinAct)) {
            //mGoSubStack.PutPosition(4); goto AddToSQLStmt; GoSubReturnPosition4:
            //sSql = sSql+"STOPPED = "+(chkNote[3].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[4].Tag==true) {
            //if (chkNote[4].Checked!=Math.Abs(mnPrvLPniSched)) {
            //mGoSubStack.PutPosition(5); goto AddToSQLStmt; GoSubReturnPosition5:
            //sSql = sSql+"LPNISCHED = "+(chkNote[4].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[5].Tag==true) {
            //if (chkNote[5].Checked!=Math.Abs(mnPrvFannieMae)) {
            //mGoSubStack.PutPosition(6); goto AddToSQLStmt; GoSubReturnPosition6:
            //sSql = sSql+"FANNIEMAE = "+(chkNote[5].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[6].Tag==true) {
            //if (chkNote[6].Checked!=Math.Abs(mnPrvForeclosure)) {
            //mGoSubStack.PutPosition(7); goto AddToSQLStmt; GoSubReturnPosition7:
            //sSql = sSql+"PFORECLOSURE = "+(chkNote[6].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[7].Tag==true) {
            //if (chkNote[7].Checked!=Math.Abs(mnPrvBankruptcy)) {
            //mGoSubStack.PutPosition(8); goto AddToSQLStmt; GoSubReturnPosition8:
            //sSql = sSql+"PBANKRUPTCY = "+(chkNote[7].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[8].Tag==true) {
            //if (chkNote[8].Checked!=Math.Abs(mnPrv203KIndicator)) {
            //mGoSubStack.PutPosition(9); goto AddToSQLStmt; GoSubReturnPosition9:
            //sSql = sSql+"LOANINDICATOR = "+(chkNote[8].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[9].Tag==true) {
            //if (chkNote[9].Checked!=Math.Abs(mnPrvRollPerm)) {
            //mGoSubStack.PutPosition(10); goto AddToSQLStmt; GoSubReturnPosition10:
            //sSql = sSql+"PROLLPERM = "+(chkNote[9].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[10].Tag==true) {
            //if (chkNote[10].Checked!=Math.Abs(mnPrvAssetMgt)) {
            //mGoSubStack.PutPosition(11); goto AddToSQLStmt; GoSubReturnPosition11:
            //sSql = sSql+"PASSETMGT = "+(chkNote[10].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[11].Tag==true) {
            //if (chkNote[11].Checked!=Math.Abs(mnPrvOriginalTerms)) {
            //mGoSubStack.PutPosition(12); goto AddToSQLStmt; GoSubReturnPosition12:
            //sSql = sSql+"PORIGTERMS = "+(chkNote[11].Checked==false ? 0 : -1);
            //}
            //}
            //if (chkNote[12].Tag==true) {
            //if (chkNote[12].Checked!=Math.Abs(mnPrvAutomaticRecast)) {
            //mGoSubStack.PutPosition(13); goto AddToSQLStmt; GoSubReturnPosition13:
            //sSql = sSql+"PAUTORECAST = "+(chkNote[12].Checked==false ? 0 : -1);
            //}
            //}
            //if (optAutoGen[0].Tag==true) {
            //mGoSubStack.PutPosition(14); goto AddToSQLStmt; GoSubReturnPosition14:
            //sSql = sSql+"AUTOGENBORFUNDS = 'D'";
            //}
            //if (optAutoGen[1].Tag==true) {
            //mGoSubStack.PutPosition(15); goto AddToSQLStmt; GoSubReturnPosition15:
            //sSql = sSql+"AUTOGENBORFUNDS = 'E'";
            //}
            //if (optAutoGen[2].Tag==true) {
            //mGoSubStack.PutPosition(16); goto AddToSQLStmt; GoSubReturnPosition16:
            //sSql = sSql+"AUTOGENBORFUNDS = ' '";
            //}
            //if (ChkOutside.Tag==true) {
            //mGoSubStack.PutPosition(17); goto AddToSQLStmt; GoSubReturnPosition17:
            //sSql = sSql+"OutsideLast = "+(ChkOutside.Checked==vbChecked ? "'Y'" : "''");
            //}
            //if (chkOmitBVInfo.Tag==true) {
            //mGoSubStack.PutPosition(18); goto AddToSQLStmt; GoSubReturnPosition18: // This Should Be VbUnchecked
            //sSql = sSql+"OmitBVOnWebInspFlag = "+(chkOmitBVInfo.Checked==false ? 0 : -1);
            //}
            //if (goSerialInfo.BorrowerPortal) {
            //if (chkDualApproval.Tag==true) {
            //mGoSubStack.PutPosition(19); goto AddToSQLStmt; GoSubReturnPosition19:
            //sSql = sSql+"DualApprovalFlag = "+(chkDualApproval.Checked==vbChecked ? "1" : "0");
            //}
            //} else {
            //}
            //if (!mblnComRuleNoUpdate &&  mblnComRuleChanged) { // Leave COM RULE Info UnChanged?
            //if (lblComRule.Tag!=mdblCommitmentRule) {
            //mGoSubStack.PutPosition(20); goto AddToSQLStmt; GoSubReturnPosition20:
            //sSql = sSql+"CommitmentRuleID = "+mdblCommitmentRule;
            //}
            //if (chkORComRule.Checked!=chkORComRule.Tag) {
            //mGoSubStack.PutPosition(21); goto AddToSQLStmt; GoSubReturnPosition21:
            //sSql = sSql+"RuleOverrideFlag = "+(mblnComRuleOverride ? -1 : 0);
            //}
            //}
            //sSql = StrUpdChgFld(mskNote[8], "PADDRESS", sSql, mskNote[8].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[9], "PCITY", sSql, mskNote[9].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[1], "PCOUNTY", sSql, mskNote[1].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[11], "PZIP", sSql, mskNote[11].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskGPSCoords[1], "PGPSCoordinate1", sSql, mskGPSCoords[1].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskGPSCoords[2], "PGPSCoordinate2", sSql, mskGPSCoords[2].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[5], "PLOT", sSql, mskNote[5].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[0], "PBLOCK", sSql, mskNote[0].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[3], "PSECTION", sSql, mskNote[3].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[6], "PPHASE", sSql, mskNote[6].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[10], "PSUBDIVIS", sSql, mskNote[10].MaxLength, Convert.ToInt32(false));
            //if (TCLHelper.Trim(mskNote[7])=="" && this.NoteType=="B") {
            //mskNote[7] = "Borrowing Base Note";
            //mskNote[7].Tag = true;
            //sSql = StrUpdChgFld(mskNote[7], "PLEGALDESC", sSql, mskNote[7].MaxLength, Convert.ToInt32(false));
            //} else {
            //sSql = StrUpdChgFld(mskNote[7], "PLEGALDESC", sSql, mskNote[7].MaxLength, Convert.ToInt32(false));
            //}
            //sSql = StrUpdChgFld(mskNote[12], "PCOTRACTOR", sSql, mskNote[12].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[13], "ACCOUNTID", sSql, mskNote[13].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[2], "PCTRACK", sSql, mskNote[2].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[4], "PCLNO", sSql, mskNote[4].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(mskNote[14], "PSPECINS1", sSql, mskNote[14].MaxLength, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[0], "PGLTABLE", sSql, 3, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[2], "PSTATE", sSql, 2, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[12], "PCOUNTRY", sSql, 3, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[5], "PFEDCD", sSql, 4, Convert.ToInt32(false));
            //if (TCLHelper.Trim(gsPayoffDate)=="") { // For RFC - 29728
            //sSql = StrUpdChgFld(cboNote[4], "PSTATUS", sSql, 1, Convert.ToInt32(false));
            //} else {
            //sSql = StrUpdChgFld(cboNote[4], "X_PSTATUS", sSql, 1, Convert.ToInt32(false));
            //}
            //sSql = StrUpdChgFld(cboNote[7], "PLCLAS", sSql, 3, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[6], "PCSHEET", sSql, 3, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[8], "PLOANTYPE", sSql, 10, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[9], "PLOANPURPOSE", sSql, 10, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[10], "PLOANCOLLATERAL", sSql, 10, Convert.ToInt32(false));
            //sSql = StrUpdChgFld(cboNote[18], "PADMINISTRATOR", sSql, 10, Convert.ToInt32(false)); // 8.11.0 - RFC 15151
            //sSql = StrUpdChgFld(ssdDates[0], "PNDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[1], "PMDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[4], "PAPPLY", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[5], "PCLOSE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[6], "PAPPROVAL", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[2], "PCDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[3], "PSDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[7], "PQDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[8], "PPDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[9], "CONVDATE", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[10], "RATELOCK", sSql, 0, Convert.ToInt32(true));
            //sSql = StrUpdChgFld(ssdDates[11], "LoanGradeDate", sSql, 0, Convert.ToInt32(true));
            //if (TCLHelper.Trim(gsPayoffDate)=="") {
            //mGoSubStack.PutPosition(22); goto AddToSQLStmt; GoSubReturnPosition22:
            //sSql = sSql+"X_PSTATUS = '' ";
            //}
            //if (mskFund.Tag==true) {
            //mGoSubStack.PutPosition(23); goto AddToSQLStmt; GoSubReturnPosition23:
            //sSql = sSql+"PPCNTFD = "+(mskFund).ToString("Fixed");
            //}
            //if (this.NoteType=="S" || this.NoteType=="D") {
            //if (mskTenant.Tag==true) {
            //mGoSubStack.PutPosition(24); goto AddToSQLStmt; GoSubReturnPosition24:
            //sSql = sSql+" TenantSpaceSF = "+TCLHelper.ConvertToInt(mskTenant.Text);
            //}
            //}
            //if (cboNote[1].Tag==true) {
            //mGoSubStack.PutPosition(25); goto AddToSQLStmt; GoSubReturnPosition25:
            //strWork = pubCBALCombo_GetValue(cboNote[1]); // RFC 28684     SaveNote()
            //sSql = sSql+"PCOMPANY = '"+SQLChar(strWork)+"'"; // RFC 28684     SaveNote()
            //}
            //if (cboNote[3].Tag==true) {
            //mGoSubStack.PutPosition(26); goto AddToSQLStmt; GoSubReturnPosition26:
            //strWork = pubCBALCombo_GetValue(cboNote[3]); // RFC 28684     SaveNote()
            //sSql = sSql+"PBRANCH = '"+SQLChar(strWork)+"'"; // RFC 28684     SaveNote()
            //}
            //Debug.WriteLine("NOTE: "+TCLHelper.Right(sSql, 45));
            //if (cboNote[13].Tag==true || cboNote[14].Tag==true) {
            //strWork = pubCBALCombo_GetValue(cboNote[13]); // AREA                          ' RFC 28684     SaveNote()
            //mGoSubStack.PutPosition(27); goto AddToSQLStmt; GoSubReturnPosition27: // AREA                          ' RFC 28684     SaveNote()
            //sSql = sSql+"PLOCMCLASS = '"+strWork+"'"; // AREA                          ' RFC 28684     SaveNote()
            //strWork2 = pubCBALCombo_GetValue(cboNote[14]); // LOCALE                        ' RFC 28684     SaveNote()
            //mGoSubStack.PutPosition(28); goto AddToSQLStmt; GoSubReturnPosition28: // LOCALE                        ' RFC 28684     SaveNote()
            //sSql = sSql+"PLOCSCLASS = '"+strWork2+"'"; // LOCALE                        ' RFC 28684     SaveNote()
            //if (strWork=="") { // NO M CLASS - NO PLOC              ' PLOC                          ' RFC 28684     SaveNote()
            //mGoSubStack.PutPosition(29); goto AddToSQLStmt; GoSubReturnPosition29: // PLOC                          ' RFC 28684     SaveNote()
            //sSql = sSql+"PLOC = ''"; // PLOC                          ' RFC 28684     SaveNote()
            //} else {						// PLOC                          ' RFC 28684     SaveNote()
            //mGoSubStack.PutPosition(30); goto AddToSQLStmt; GoSubReturnPosition30: // PLOC                          ' RFC 28684     SaveNote()
            //sSql = sSql+"PLOC = '"+strWork+strWork2+"'"; // PLOC                          ' RFC 28684     SaveNote()
            //} // PLOC                          ' RFC 28684     SaveNote()
            //}
            //if (cboNote[15].Tag==true || cboNote[16].Tag==true) {
            //if (TCLHelper.GetData(SelectedClass())=="0000") {
            //mGoSubStack.PutPosition(31); goto AddToSQLStmt; GoSubReturnPosition31:
            //sSql = sSql+"PCLASS = ''";
            //mGoSubStack.PutPosition(32); goto AddToSQLStmt; GoSubReturnPosition32:
            //sSql = sSql+"PPRJMCLASS = ''";
            //mGoSubStack.PutPosition(33); goto AddToSQLStmt; GoSubReturnPosition33:
            //sSql = sSql+"PPRJSCLASS = ''";
            //} else {
            //mGoSubStack.PutPosition(34); goto AddToSQLStmt; GoSubReturnPosition34:
            //sSql = sSql+"PCLASS = '"+SQLChar(SelectedClass())+"'";
            //mGoSubStack.PutPosition(35); goto AddToSQLStmt; GoSubReturnPosition35:
            //sSql = sSql+"PPRJMCLASS = '"+(TCLHelper.ConvertToInt(aClassMaj[cboNote[15].SelectedIndex])).ToString("00")+"'";
            //mGoSubStack.PutPosition(36); goto AddToSQLStmt; GoSubReturnPosition36:
            //sSql = sSql+"PPRJSCLASS = '"+(TCLHelper.ConvertToInt(aClassMin[cboNote[16].SelectedIndex])).ToString("00")+"'";
            //}
            //}
            //if (cboInspCom.Tag==true) {
            //mGoSubStack.PutPosition(37); goto AddToSQLStmt; GoSubReturnPosition37:
            //sSql = sSql+"COMPANYID= "+Microsoft.VisualBasic.Compatibility.VB6.Support.GetItemData(cboInspCom, cboInspCom.SelectedIndex);
            //}
            //if (Convert.ToBoolean(bRenewal)) {
            //mGoSubStack.PutPosition(38); goto AddToSQLStmt; GoSubReturnPosition38:
            //sSql = sSql+"PRENEW = "+(nRenewalCount).ToString();
            //}
            //if (TCLHelper.ConvertToInt(aCreditMasterLines[cboNote[11].SelectedIndex])!=mdblPrvLOCMID) {
            //mGoSubStack.PutPosition(39); goto AddToSQLStmt; GoSubReturnPosition39:
            //sSql = sSql+"LOCMID = "+TCLHelper.ConvertToInt(aCreditMasterLines[cboNote[11].SelectedIndex])+"";
            //blnLOCSEQ = true;
            //}
            //if (aCreditSubLines[cboNote[17].SelectedIndex]!=sPrvLCSEQ) {
            //mGoSubStack.PutPosition(40); goto AddToSQLStmt; GoSubReturnPosition40:
            //sSql = sSql+"PLCSEQ = '"+SQLChar(aCreditSubLines[cboNote[17].SelectedIndex])+"'";
            //blnLOCSEQ = true;
            //}
            //if (TCLHelper.UCase(this.NoteMode)=="PIPELINE") {
            //mGoSubStack.PutPosition(41); goto AddToSQLStmt; GoSubReturnPosition41:
            //sSql = sSql+"PCLAMT = "+mskFin[10];
            //sSql = sSql+", PBDAMT = "+mskFin[11];
            //sSql = sSql+", PBEAMT = "+mskFin[12];
            //sSql = sSql+", PCCAMT = "+mskFin[13];
            //sSql = sSql+", PCOAMT = "+mskFin[14];
            //sSql = sSql+", POSSREQD = "+mskFin[15];
            //sSql = sSql+", PCLORG = "+mskFin[10];
            //sSql = sSql+", PBDORG = "+mskFin[11];
            //sSql = sSql+", PBEORG = "+mskFin[12];
            //sSql = sSql+", PCCORG = "+mskFin[13];
            //sSql = sSql+", PCOORG = "+mskFin[14];
            //sSql = sSql+", PCPAMT = "+mskFin[20];
            //} else {
            //if (this.UnitNumber=="000") {
            //mGoSubStack.PutPosition(42); goto AddToSQLStmt; GoSubReturnPosition42:
            //sSql = sSql+"PCLAMT = "+mskFin[10];
            //sSql = sSql+", PBDAMT = "+mskFin[11];
            //sSql = sSql+", PBEAMT = "+mskFin[12];
            //}
            //if (this.Action==1) {
            //mGoSubStack.PutPosition(43); goto AddToSQLStmt; GoSubReturnPosition43:
            //sSql = sSql+"PCLORG = "+mskFin[10];
            //sSql = sSql+", PBDORG = "+mskFin[11];
            //sSql = sSql+", PBEORG = "+mskFin[12];
            //sSql = sSql+", PCCORG = "+mskFin[13];
            //sSql = sSql+", PCOORG = "+mskFin[14];
            //}
            //if (mskFin[19]!=0) {
            //if (TCLHelper.InStr(1, "DMS", this.NoteType, vbTextCompare)>0) {
            //mGoSubStack.PutPosition(44); goto AddToSQLStmt; GoSubReturnPosition44:
            //sSql = sSql+"PCPAMT = "+mskFin[20];
            //}
            //}
            //}
            //if (goSerialInfo.BorrowingBase &&  this.NoteType=="B") {
            //if (chkUseInspPct.Tag==true) {
            //mGoSubStack.PutPosition(45); goto AddToSQLStmt; GoSubReturnPosition45:
            //sSql = Convert.ToString(sSql+"BBUseInspPctComplete = "+chkUseInspPct.Checked);
            //}
            //if (chkBBNewInPipeline.Tag==true) {
            //mGoSubStack.PutPosition(46); goto AddToSQLStmt; GoSubReturnPosition46:
            //sSql = Convert.ToString(sSql+"BBNewInPipeline = "+chkBBNewInPipeline.Checked);
            //}
            //if (VBtoConverter.CBool(ssdAuditLog[0].Tag) && (ssdAuditLog[0].Text!="")) {
            //if (!CompareDates(TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBReconcileDate"].ToString()), "=", TCLHelper.ConvertToDateTime(ssdAuditLog[0].Text))) {
            //if (CompareDates(TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBReconcileDate"].ToString()), ">", TCLHelper.ConvertToDateTime(ssdAuditLog[0].Text))) {
            //if (MessageBox.Show("The Reconcile Date entered is early than the previous date, are you sure you want to update it?", null, vbQuestion+vbYesNo, vbQuestion+vbYesNo)==vbYes) {
            //sSql = StrUpdChgFld(ssdAuditLog[0], "BBReconcileDate", sSql, 0, Convert.ToInt32(true));
            //} else {
            //ssdAuditLog[0].Tag = false;
            //ssdAuditLog[0].Text = TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBReconcileDate"].ToString());
            //}
            //} else {
            //sSql = StrUpdChgFld(ssdAuditLog[0], "BBReconcileDate", sSql, 0, Convert.ToInt32(true));
            //}
            //} else {
            //ssdAuditLog[0].Tag = false;
            //ssdAuditLog[0].Text = "";
            //}
            //} else {
            //}
            //if (VBtoConverter.CBool(ssdAuditLog[1].Tag) && (ssdAuditLog[1].Text!="")) {
            //if (!CompareDates(TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBAuditDate"].ToString()), "=", TCLHelper.ConvertToDateTime(ssdAuditLog[1].Text))) {
            //if (CompareDates(TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBAuditDate"].ToString()), ">", TCLHelper.ConvertToDateTime(ssdAuditLog[1].Text))) {
            //if (MessageBox.Show("The Audit Date entered is early than the previous date, are you sure you want to update it?", null, vbQuestion+vbYesNo, vbQuestion+vbYesNo)==vbYes) {
            //sSql = StrUpdChgFld(ssdAuditLog[1], "BBAuditDate", sSql, 0, Convert.ToInt32(true));
            //} else {
            //ssdAuditLog[1].Tag = false;
            //ssdAuditLog[1].Text = TCLHelper.ConvertToDateTime(adoSetupModTable.Fields["BBAuditDate"].ToString());
            //}
            //} else {
            //sSql = StrUpdChgFld(ssdAuditLog[1], "BBAuditDate", sSql, 0, Convert.ToInt32(true));
            //}
            //} else {
            //ssdAuditLog[1].Tag = false;
            //ssdAuditLog[1].Text = "";
            //}
            //} else {
            //}
            //} else {
            //}
            //if (cmdVendor.Tag==true) {
            //mGoSubStack.PutPosition(47); goto AddToSQLStmt; GoSubReturnPosition47:
            //sSql = sSql+"PVENDOR = '"+SQLChar(msVendor)+"'";
            //}
            //Update_Now: ;
            //if (sSql!="") {
            //mGoSubStack.PutPosition(48); goto AddToSQLStmt; GoSubReturnPosition48:
            //sSql = sSql+"PTRAN = "+SQLDate(pubGetDateLocalized);
            //sSql = sSql+", PUSER = '"+gsUserName+"'";
            //sSql = "UPDATE "+this.NoteMode+" SET "+sSql;
            //sSql = sSql+" WHERE PNOTENO = '"+SQLChar(this.NoteNumber);
            //sSql = sSql+"' AND PUNIT = '"+SQLChar(this.UnitNumber)+"'";
            //nRows = SQLExec(false, sSql, goUserConnect.Driver);
            //strWork = pubCBALCombo_GetValue(cboNote[1]);
            //sSql = "ACOMPANY = '"+SQLChar(strWork)+"'"; // RFC 28684     SaveNote()
            //mGoSubStack.PutPosition(49); goto AddToSQLStmt; GoSubReturnPosition49:
            //strWork = pubCBALCombo_GetValue(cboNote[3]);
            //sSql = "ABRANCH = '"+SQLChar(strWork)+"'"; // RFC 28684     SaveNote()
            //Debug.WriteLine("ADV: "+TCLHelper.Right(sSql, 45));
            //sSql = "UPDATE ADVANCE SET "+sSql;
            //sSql = sSql+" WHERE ANOTE = '"+SQLChar(this.NoteNumber);
            //sSql = sSql+"' AND AUNIT = '"+SQLChar(this.UnitNumber)+"'";
            //nRows = SQLExec(false, sSql, goUserConnect.Driver);
            //Debug.WriteLine("UPD: "+sSql + Environment.NewLine + Conversion.Str(nRows));
            //}
            //DBCommit();
            this.noteInfoPresenter.SaveNote(FillSaveNoteValues());
            //**********************UPTO THIS CALL SAVENOTE****************************//

            if (this.bLOCIntProfAdd == true)
            {
                //if (adoINOTE.RecordCount==0) 
                //{
                this.noteInfoPresenter.AddLocIntProf(this.BorrowerNo, this.NoteNumber, this.UnitNumber, TCLHelper.ConvertToDouble(this.dblMasterLookupIntProf), this.sSubLookupIntProf, true, this.noteInfoPresenter.GetDateLocalized(false));
                //AddLOCIntProf(TCLHelper.GetData(adoSetupModTable("PBNUMBER")), dblMasterLookupIntProf, sSubLookupIntProf, TCLHelper.GetData(adoSetupModTable("PNOTENO")), TCLHelper.GetData(adoSetupModTable("PUNIT")), pubGetDateLocalized, true);
                //}
            }

            if (this.bLOCEqtProfAdd == true)
            {
                //if (rsEqtyProf.RecordCount==0) 
                //{ 
                this.noteInfoPresenter.AddLocEqtProf(this.BorrowerNo, this.NoteNumber, this.UnitNumber, TCLHelper.ConvertToDouble(this.dblMasterLookupIntProf), this.sSubLookupIntProf, true, this.noteInfoPresenter.GetDateLocalized(false));
                //AddLOCEqtProf(TCLHelper.GetData(adoSetupModTable("PBNUMBER")), dblMasterLookupIntProf, sSubLookupIntProf, TCLHelper.GetData(adoSetupModTable("PNOTENO")), TCLHelper.GetData(adoSetupModTable("PUNIT")), pubGetDateLocalized, true);
                //}
            }

            if (TCLHelper.UCase(this.NoteMode) == "PROPERTY" && (TCLHelper.ConvertToDouble(ddlMLoc.GetSelectedValue()) != TCLHelper.ConvertToDouble(this.dblMasterLookupIntProf) || TCLHelper.ConvertToDouble(ddlSLoc.GetSelectedValue()) != TCLHelper.ConvertToDouble(this.sSubLookupIntProf)))
            {
                DoSubs = Convert.ToInt32(false);
                if (this.UnitNumber == "000" && this.Action == 2)
                {
                    //if (MessageBox.Show("Do you want to attach all sub notes to this new Line-of-Credit?", null, vbCritical+vbYesNo, vbCritical+vbYesNo)==vbYes) 
                    //{
                    //DoSubs = Convert.ToInt32(true);
                    //} 
                    //else 
                    //{
                    //DoSubs = Convert.ToInt32(false);
                    //}
                }
            }

            //CALL SAVENOTETWO

            Dictionary<string, string> dictSaveNo2Params = new Dictionary<string, string>();
            dictSaveNo2Params.Add("gsNoteType", this.NoteMode);
            dictSaveNo2Params.Add("PBNUMBER", this.BorrowerNo);
            dictSaveNo2Params.Add("PNOTENO", this.NoteNumber);
            dictSaveNo2Params.Add("PUNIT", this.UnitNumber);
            dictSaveNo2Params.Add("mdblPrvLOCMID", this.dblMasterLookupIntProf);
            dictSaveNo2Params.Add("sPrvLCSEQ", this.sSubLookupIntProf);
            dictSaveNo2Params.Add("DoSubs", this.DoSubs.ToString());
            dictSaveNo2Params.Add("mskFin10", txtFincTabLoanCommit3.Text);
            dictSaveNo2Params.Add("prsamt_d", this.prsamt_d);
            dictSaveNo2Params.Add("pcfamt", this.pcfamt);
            dictSaveNo2Params.Add("PCLAMT_D", this.PCLAMT_D);
            dictSaveNo2Params.Add("LOCMID", ddlMLoc.GetSelectedValue());
            dictSaveNo2Params.Add("PLCSEQ", ddlSLoc.GetSelectedValue());
            dictSaveNo2Params.Add("mskFin3", txtFincTabLoanCommit2.Text);
            this.noteInfoPresenter.SaveNoteTwo(dictSaveNo2Params);

            //***************************CALL SP uspSaveNotetwo ********************************END HERE
            string sType = string.Empty;
            string sICode = string.Empty;
            string Memo = string.Empty;
            string sEqtyTranType = string.Empty;
            string Off = string.Empty;
            double Amt = 0;
            string vEff = string.Empty;
            string Tran = string.Empty;
            int TranNum = 0;
            int nRows = 0;
            if (TCLHelper.UCase(this.NoteMode) != "PIPELINE" && this.UnitNumber != "000")
            {
                if (this.Action == 1)
                {
                    sType = "2";
                }
                else
                {
                    sType = "4";
                }
                TranNum = 0;
                nRows = 3;
                int[] mskFin = null;
                //while (nRows < 6)
                //{
                //    if (mskFin[nRows] != 0)
                //    {
                //        if (TranNum != 0)
                //        {
                //            //TranNum = SetTranNum();
                //        }
                //        if (this.Action == 1)
                //        {
                //            switch (nRows)
                //            {
                //                case 3:
                //                    {
                //                        sICode = "N";
                //                        Memo = "Commitment Setup";
                //                        sEqtyTranType = "";
                //                        break;
                //                    }
                //                case 4:
                //                    {
                //                        sICode = "O";
                //                        Memo = "Note Level Deposit Setup";
                //                        sEqtyTranType = "D";
                //                        break;
                //                    }
                //                case 5:
                //                    {
                //                        sICode = "P";
                //                        Memo = "Note Level Escrow Setup";
                //                        sEqtyTranType = "D";
                //                        break;
                //                    }
                //            } //end switch
                //        }
                //        else
                //        {
                //            switch (nRows)
                //            {
                //                case 3:
                //                    {
                //                        sICode = "T";
                //                        Memo = "Commitment Adjustment";
                //                        sEqtyTranType = "";
                //                        break;
                //                    }
                //                case 4:
                //                    {
                //                        sICode = "Q";
                //                        Memo = "Note Level Deposit Adjustment";
                //                        sEqtyTranType = "D";
                //                        break;
                //                    }
                //                case 5:
                //                    {
                //                        sICode = "R";
                //                        Memo = "Note Level Escrow Adjustment";
                //                        sEqtyTranType = "D";
                //                        break;
                //                    }
                //            } //end switch
                //        }
                //        Off = "";
                //        Amt = mskFin[nRows];
                //        switch (nRows)
                //        {
                //            case 3:
                //                {
                //                    vEff = txtFincTabEffctDate1.Text; //ssdEffective[0].Text;
                //                    //Tran = cboTranCode[0].Tag;
                //                    break;
                //                }
                //            case 4:
                //                {
                //                    vEff = txtFincTabEffctDate1.Text;
                //                    //Tran = TCLHelper.Trim(cboTranCode[1].Tag);
                //                    break;
                //                }
                //            case 5:
                //                {
                //                    vEff = txtFincTabEffctDate1.Text;
                //                    //Tran = TCLHelper.Trim(cboTranCode[2].Tag);
                //                    break;
                //                }
                //        } //end switch

                //        //if (!PostTrans(this.NoteNumber, this.UnitNumber, sType, sICode, vEff, Off, Amt, Memo, "", "", "", Tran, TranNum, "", false, false, "", "", "", "", "", "", false, sEqtyTranType, "", "", 0, "", "", 0, gsUserName, false, false, ""))
                //        //{
                //        //MessageBox.Show("An error occured trying to post transaction detail for " + Memo);
                //        //}
                //    }

                //    nRows += 1;
                //}
            }

            //*************SAVENOTETHREE*********START
            Dictionary<string, string> inputParams = new Dictionary<string, string>();
            inputParams.Add("gsNoteType", this.NoteMode);
            inputParams.Add("PBNUMBER", this.BorrowerNo);
            inputParams.Add("PNOTENO", this.NoteNumber);
            inputParams.Add("PUNIT", this.UnitNumber);
            inputParams.Add("mskFin10", txtFincTabLoanCommit3.Text);
            inputParams.Add("pcfamt", this.pcfamt);
            inputParams.Add("PCLAMT_D", this.PCLAMT_D);
            inputParams.Add("mskFin9", txtFincTabConstAdjsmnt.Text);
            inputParams.Add("mskFin14", txtFincTabConstRslt.Text);
            inputParams.Add("chkNote8", ddlLoanType.GetSelectedText());
            inputParams.Add("bRenewal", this.bRenewal.ToString());//brenewal need to assign
            inputParams.Add("sRenewal", string.Empty);//need to assign
            inputParams.Add("lblLabel11", string.Empty);//BorrowerName
            inputParams.Add("ssdDates0", txtDateTabPrssNote.Text);
            inputParams.Add("ssdDates1", txtDateTabMturty.Text);
            inputParams.Add("dPrevMatDate", this.dPrevMatDate);//need to assign
            inputParams.Add("nRenewalCount", this.nRenewalCount.ToString());//need to assign
            inputParams.Add("mskNote7", txtPrjctShrtLglDesc.Text);
            inputParams.Add("gsUserName", this.UserName);
            inputParams.Add("chkNote2tag", "1");//need to assign
            inputParams.Add("chkNote2", chkInDefault.GetTCLValueInteger().ToString());
            inputParams.Add("mnPrvInDefault", string.Empty); //chkInDefault.GetTCLValue());//need to check
            inputParams.Add("srtnDate", this.noteInfoPresenter.GetDateLocalized(false));
            inputParams.Add("gsFDate", this.PFDATE);
            inputParams.Add("chkNote3tag", "1"); //need to assign
            inputParams.Add("chkNote3", chkStopFin.GetTCLValueInteger().ToString());
            inputParams.Add("mnPrvStopFinAct", string.Empty);
            inputParams.Add("TranNum", string.Empty); //need to assign values
            inputParams.Add("mskFin16", txtFincTabOutEqtyAdjstmnt.Text);
            inputParams.Add("mskFin8", txtFincTabTotlAdjsmnt.Text);
            inputParams.Add("RecID", new CommonService("ACC04").RecordID().ToString());
            string errormsg = string.Empty;
            noteInfoPresenter.SaveNotethree(inputParams, out errormsg);
            //CALL SAVENOTE THREE ENDS*******************************

            //Status_End();
            if (this.NoteType == "B")
            {
            }

            //if (goDraprof.bln_AUDITRPT)
            //{
            //AuditRpt();
            //}

            //Close();
            return;
        }

        public Dictionary<string, string> FillSaveNoteValues()
        {
            Dictionary<string, string> inputParams = new Dictionary<string, string>();
            inputParams.Add("gsNoteType", this.NoteMode);
            inputParams.Add("PNOTENO", this.NoteNumber);
            inputParams.Add("PUNIT", this.UnitNumber);
            inputParams.Add("PPTYPE", chkRevolving.GetTCLValueString());
            inputParams.Add("PNOACCRUAL", chkNonAccural.GetTCLValueInteger().ToString());
            inputParams.Add("PINDEFAULT", chkInDefault.GetTCLValueInteger().ToString());
            inputParams.Add("STOPPED", chkStopFin.GetTCLValueInteger().ToString());
            //inputParams.Add("LPNISCHED", chkAmortizeLoan.GetTCLValueInteger().ToString());
            //inputParams.Add("FANNIEMAE", chkFannieMae.GetTCLValueInteger().ToString());
            inputParams.Add("PFORECLOSURE", chkForeclosure.GetTCLValueInteger().ToString());
            inputParams.Add("PBANKRUPTCY", chkBankruptcy.GetTCLValueInteger().ToString());
            inputParams.Add("LOANINDICATOR", chk203K.GetTCLValueInteger().ToString());
            inputParams.Add("PROLLPERM", chkRollToPerm.GetTCLValueInteger().ToString());
            inputParams.Add("PASSETMGT", chkAssetManagementt.GetTCLValueInteger().ToString());
            //inputParams.Add("PORIGTERMS", chkOriginal.GetTCLValueInteger().ToString());
            //inputParams.Add("PAUTORECAST", chkAutomatic.GetTCLValueInteger().ToString());
            inputParams.Add("AUTOGENBORFUNDS", ddlAutoGenBrwFndFirst.GetSelectedValue());
            inputParams.Add("OutsideLast", chkOutside.GetTCLValueString());
            inputParams.Add("OmitBVOnWebInspFlag", chkOmit.GetTCLValueInteger().ToString());
            inputParams.Add("DualApprovalFlag", chkDualAprvl.GetTCLValueInteger().ToString());
            inputParams.Add("CommitmentRuleID", lblComRule.Text);
            inputParams.Add("RuleOverrideFlag", chkORComRule.GetTCLValueInteger().ToString());
            inputParams.Add("PADDRESS", txtPrjctStrtAddrs.Text);
            inputParams.Add("PCITY", txtPrjctCity.Text);
            inputParams.Add("PCOUNTY", txtPrjctCounty.Text);
            inputParams.Add("PZIP", txtPrjctZipCode.Text);
            inputParams.Add("PGPSCoordinate1", txtPrjctGPS.Text);
            inputParams.Add("PGPSCoordinate2", txtPrjctGPS1.Text);
            inputParams.Add("PLOT", txtPrjctLot.Text);
            inputParams.Add("PBLOCK", txtPrjctBlock.Text);
            inputParams.Add("PSECTION", txtPrjctSection.Text);
            inputParams.Add("PPHASE", txtPrjctPhase.Text);
            inputParams.Add("PSUBDIVIS", txtPrjctSubDiv.Text);
            inputParams.Add("PLEGALDESC", txtPrjctShrtLglDesc.Text);
            inputParams.Add("PCOTRACTOR", txtPrjctPrimryContrct.Text);
            inputParams.Add("ACCOUNTID", txtPrjctAccID.Text);
            inputParams.Add("PCTRACK", txtCensusTest.Text);
            inputParams.Add("PCLNO", txtCommitment.Text);
            inputParams.Add("PSPECINS1", txtPrjctPurchLoan.Text);
            inputParams.Add("PGLTABLE", ddlGLTable.GetSelectedText());
            inputParams.Add("PSTATE", drpdwnlstState.GetSelectedText());
            inputParams.Add("PCOUNTRY", drpdwnlstCountry.GetSelectedText());
            inputParams.Add("PFEDCD", ddlFederalCode.GetSelectedText());
            inputParams.Add("PSTATUS", ddlStatus.GetSelectedText());
            inputParams.Add("X_PSTATUS", ddlStatus.GetSelectedText());
            inputParams.Add("PLCLAS", ddlLoanClass.GetSelectedText());
            inputParams.Add("PCSHEET", ddlLoanGrade.GetSelectedText());
            inputParams.Add("PLOANTYPE", ddlLoanType.GetSelectedText());
            inputParams.Add("PLOANPURPOSE", ddlLoanPurpose.GetSelectedText());
            inputParams.Add("PLOANCOLLATERAL", ddlCollateralCode.GetSelectedText());
            inputParams.Add("PADMINISTRATOR", drpdwnlstAdmin.GetSelectedText());
            inputParams.Add("PNDATE", txtDateTabPrssNote.Text);
            inputParams.Add("PMDATE", txtDateTabMturty.Text);
            inputParams.Add("PAPPLY", txtDateTabApplc.Text);
            inputParams.Add("PCLOSE", txtDateTabClsng.Text);
            inputParams.Add("PAPPROVAL", txtDateTabApprvl.Text);
            inputParams.Add("PCDATE", txtDateTabCnsCmpl.Text);
            inputParams.Add("PSDATE", txtDateTabCnsStart.Text);
            inputParams.Add("PQDATE", txtDateTabQotPayOff.Text);
            inputParams.Add("PPDATE", txtDateTabQotPost.Text);
            inputParams.Add("CONVDATE", txtDateTabconvrs.Text);
            inputParams.Add("RATELOCK", txtDateTabRateLck.Text);
            inputParams.Add("LoanGradeDate", txtLoanGrdDate.Text);
            inputParams.Add("PPCNTFD", txtDateTabPrcntFund.Text);
            inputParams.Add("TenantSpaceSF", txtPrjctNetRntArea.Text);
            inputParams.Add("PCOMPANY", ddlCompany.GetSelectedValue());
            inputParams.Add("PBRANCH", ddlBranch.GetSelectedValue());
            inputParams.Add("PLOCMCLASS", ddlArea.GetSelectedValue());
            inputParams.Add("PLOCSCLASS", ddlLocal.GetSelectedValue());
            inputParams.Add("PLOC", ddlArea.GetSelectedText());

            string mClass = ddlMClass.GetSelectedValue();
            string sClass = ddlSClass.GetSelectedValue();
            if (string.IsNullOrEmpty(sClass) == false) mClass = mClass + sClass;
            inputParams.Add("PCLASS", mClass);

            inputParams.Add("PPRJMCLASS", ddlMClass.GetSelectedValue());
            inputParams.Add("PPRJSCLASS", ddlSClass.GetSelectedValue());
            inputParams.Add("COMPANYID", ddlInspCompany.GetSelectedValue());

            inputParams.Add("PRENEW", this.bRenewal.ToString());

            inputParams.Add("LOCMID", ddlMLoc.GetSelectedValue());
            inputParams.Add("PLCSEQ", ddlSLoc.GetSelectedValue());
            inputParams.Add("PCLAMT", txtFincTabLoanCommit3.Text);
            inputParams.Add("PBDAMT", txtFincTabLnLvlDpst3.Text);
            inputParams.Add("PBEAMT", txtFincTabLnLvlEscrw3.Text);
            inputParams.Add("PCCAMT", txtFincTabTotlRslt.Text);
            inputParams.Add("PCOAMT", txtFincTabConstRslt.Text);
            inputParams.Add("POSSREQD", txtFincTabOutEqtyRslt.Text);
            inputParams.Add("PCLORG", txtFincTabLoanCommit3.Text);
            inputParams.Add("PBDORG", txtFincTabLnLvlDpst3.Text);
            inputParams.Add("PBEORG", txtFincTabLnLvlEscrw3.Text);
            inputParams.Add("PCCORG", txtFincTabTotlRslt.Text);
            inputParams.Add("PCOORG", txtFincTabConstRslt.Text);
            inputParams.Add("PCPAMT", txtFincTabprincBal3.Text);
            inputParams.Add("BBUseInspPctComplete", "");
            inputParams.Add("BBNewInPipeline", "");
            inputParams.Add("BBReconcileDate", "");
            inputParams.Add("BBAuditDate", "");
            inputParams.Add("PVENDOR", "");
            inputParams.Add("PTRAN", "");
            inputParams.Add("PUSER", "");
            inputParams.Add("GNOTEACTION", Convert.ToString(this.Action));
            return inputParams;
        }

        protected void btnSaveDoc_Click(object sender, EventArgs e)
        {
            NewBorrwerPresenter borrowerPresenter = new NewBorrwerPresenter(this);
            try
            {
                int intExists = 0;
                Dictionary<string, string> inputParams = new Dictionary<string, string>();
                inputParams.Add("doc2note", this.NoteNumber);
                inputParams.Add("doc2unit", this.UnitNumber);
                inputParams.Add("doc2id", Convert.ToString(hdnDocId.Value).Trim());
                inputParams.Add("doc2item", Convert.ToString(txtDocGroupId.Text).Trim());
                inputParams.Add("doc2line", "00");
                inputParams.Add("doc1desc", Convert.ToString(txtDocDesc.Text));
                inputParams.Add("doc2pri", txtPri.Text);
                inputParams.Add("doc2days", txtBorDays.Text);
                inputParams.Add("doc2ldate", DBNull.Value.ToString());
                inputParams.Add("doc2ddate", DBNull.Value.ToString());
                inputParams.Add("doc2tran", string.Empty);
                inputParams.Add("doc2user", string.Empty);
                inputParams.Add("vnumber", string.Empty);
                inputParams.Add("flag", (3).ToString());
                inputParams.Add("exists", (-1).ToString());
                borrowerPresenter.uspDocInsert(inputParams, out intExists);
                if (intExists == 1)
                {
                    mpopupDocAdd.Show();
                    ScriptManager.RegisterStartupScript(Page, Page.GetType(), "Script", "alert('Group ID already exists, cannot be added.');", true);
                    return;
                }
                mpopupDocAdd.Hide();
                noteInfoPresenter = new NoteInfoPresenter(this);
                this.noteInfoPresenter.LoadDocAttach();
                lstbArtchBrwDocTrack.DataBind();
                imgbtnDocTracEdit.Visible = false;
                imgbtnDocTracAdd.Visible = false;

                string strNewDocId = Convert.ToString(hdnDocId.Value).Trim() + Convert.ToString(txtDocGroupId.Text).Trim();
                sessionProvider.Set("DOCTRACKDOCID", strNewDocId);
                sessionProvider.Set("DOCTRACKNAME", Convert.ToString(txtDocDesc.Text));

                ScriptManager.RegisterStartupScript(Page, Page.GetType(), "Script", "WDocOpen();", true);
            }
            catch (Exception ex)
            {
                Logger.LogException(ex, Level.Error);

            }
        }

        protected void btnDocCancel_Click(object sender, EventArgs e)
        {

        }
        protected void imgbtnDocTracEdit_Click(object sender, ImageClickEventArgs e)
        {
            sessionProvider.Set("DOCTRACKDOCID", Convert.ToString(hdnDocId.Value).Trim());
            sessionProvider.Set("DOCTRACKNAME", Convert.ToString(txtDocDesc.Text));
            ScriptManager.RegisterStartupScript(Page, Page.GetType(), "Script", "WDocOpen();", true);
        }

        protected void imgbtnDocTracAdd_Click(object sender, ImageClickEventArgs e)
        {
            lblDocNoteNo.Text = this.NoteNumber;
            lblDocUnit.Text = this.UnitNumber;
            txtDocDesc.Text = string.Empty;
            txtPri.Text = string.Empty;
            txtBorDays.Text = string.Empty;
            lblDocId.Text = TCLHelper.GetData(ViewState["DocId"]);
            int intGroupId = 1;
            using (DataSet dsDocMaxId = noteInfoPresenter.GetDocumentMaxId(this.NoteNumber, this.UnitNumber, Convert.ToString(hdnDocId.Value), 1))
            {
                if (TCLHelper.IsValidDataColumn(dsDocMaxId))
                {
                    if (dsDocMaxId.Tables[0].Rows.Count > 0)
                        intGroupId = TCLHelper.ConvertToInt(dsDocMaxId.Tables[0].Rows[0]["MAXITEM"]) + 1;

                }
            }
            txtDocGroupId.Text = intGroupId.ToString("D2");
            mpopupDocAdd.Show();
        }
        //protected void btnRelSchdleOKPopup_Click(object sender, EventArgs e)
        //{
        //    if (rdReleaseSchedule.SelectedValue == "0")
        //        ScriptManager.RegisterStartupScript(Page, this.GetType(), "Open", "javascript:Open();", true);
        //    else
        //    {

        //        sessionProvider.Set("rsitem",Convert.ToString(hdnItemID.Value));
        //        ScriptManager.RegisterStartupScript(Page, this.GetType(), "OpenSingle", "javascript:OpenSingle();", true);

        //    }
        //}

        #endregion

        private void HideMessagePanel()
        {
            tblMsgMPopup.Visible = false;
            trAlertSuccess.Visible = false;
            lblSuccess.Text = string.Empty;
            lblSuccess.Visible = false;
            ErrorAlert1.Visible = false;
            lblErrorAlert.Visible = false;
            lblErrorAlert.Text = string.Empty;
        }
    }
}



Designer :

---------

//------------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by a tool.
//     Runtime Version:2.0.50727.5420
//
//     Changes to this file may cause incorrect behavior and will be lost if
//     the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------

namespace ISGN.TCL.Web.Modules.DailyProcessing {
    
    
    public partial class NotesInfo {
        
        /// <summary>
        /// ToolkitScriptManager1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ToolkitScriptManager ToolkitScriptManager1;
        
        /// <summary>
        /// upanel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.UpdatePanel upanel;
        
        /// <summary>
        /// tblMsg control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTable tblMsg;
        
        /// <summary>
        /// ErrorSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow ErrorSuccess;
        
        /// <summary>
        /// lblErrorSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblErrorSuccess;
        
        /// <summary>
        /// ErrorFail control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow ErrorFail;
        
        /// <summary>
        /// lblErrorFail control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblErrorFail;
        
        /// <summary>
        /// lblBrwName control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblBrwName;
        
        /// <summary>
        /// imgbtnBrwinfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnBrwinfo;
        
        /// <summary>
        /// TabNoteInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer TabNoteInfo;
        
        /// <summary>
        /// tabPnlProject control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlProject;
        
        /// <summary>
        /// pnlPurchAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlPurchAdd;
        
        /// <summary>
        /// txtPrjctStrtAddrs control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctStrtAddrs;
        
        /// <summary>
        /// txtPrjctCity control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctCity;
        
        /// <summary>
        /// txtPrjctCounty control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctCounty;
        
        /// <summary>
        /// drpdwnlstState control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLDropDownList drpdwnlstState;
        
        /// <summary>
        /// txtPrjctZipCode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPrjctZipCode;
        
        /// <summary>
        /// FilteredTextBoxExtender14 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender14;
        
        /// <summary>
        /// drpdwnlstCountry control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList drpdwnlstCountry;
        
        /// <summary>
        /// txtPrjctShrtLglDesc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctShrtLglDesc;
        
        /// <summary>
        /// pnlSubDivision control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlSubDivision;
        
        /// <summary>
        /// txtPrjctSubDiv control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctSubDiv;
        
        /// <summary>
        /// txtPrjctPurchLoan control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctPurchLoan;
        
        /// <summary>
        /// btnPrjctUseDfndfld control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnPrjctUseDfndfld;
        
        /// <summary>
        /// hdnBorrowerNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnBorrowerNo;
        
        /// <summary>
        /// pnlPrimaryContractor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlPrimaryContractor;
        
        /// <summary>
        /// txtPrjctPrimryContrct control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPrjctPrimryContrct;
        
        /// <summary>
        /// imgbtnPrjctVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnPrjctVendor;
        
        /// <summary>
        /// chkDualAprvl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkDualAprvl;
        
        /// <summary>
        /// lblBorrowingBaseMsg control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblBorrowingBaseMsg;
        
        /// <summary>
        /// pnlGps control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlGps;
        
        /// <summary>
        /// txtPrjctGPS control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctGPS;
        
        /// <summary>
        /// txtPrjctGPS1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctGPS1;
        
        /// <summary>
        /// txtPrjctAccID control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctAccID;
        
        /// <summary>
        /// drpdwnlstAdmin control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLDropDownList drpdwnlstAdmin;
        
        /// <summary>
        /// pnlLotSec control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlLotSec;
        
        /// <summary>
        /// txtPrjctLot control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctLot;
        
        /// <summary>
        /// txtPrjctBlock control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctBlock;
        
        /// <summary>
        /// txtPrjctSection control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctSection;
        
        /// <summary>
        /// txtPrjctPhase control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctPhase;
        
        /// <summary>
        /// pnlTenantSpace control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlTenantSpace;
        
        /// <summary>
        /// txtPrjctNetRntArea control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtPrjctNetRntArea;
        
        /// <summary>
        /// btnPjrctLeasingInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnPjrctLeasingInfo;
        
        /// <summary>
        /// btnPrjctApprslInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnPrjctApprslInfo;
        
        /// <summary>
        /// btnprjctSalescntrct control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnprjctSalescntrct;
        
        /// <summary>
        /// tabPnlGeneral control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlGeneral;
        
        /// <summary>
        /// ddlCompany control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlCompany;
        
        /// <summary>
        /// ddlBranch control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlBranch;
        
        /// <summary>
        /// ddlArea control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlArea;
        
        /// <summary>
        /// ddlLocal control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlLocal;
        
        /// <summary>
        /// ddlMClass control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlMClass;
        
        /// <summary>
        /// ddlSClass control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlSClass;
        
        /// <summary>
        /// ddlMLoc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlMLoc;
        
        /// <summary>
        /// ddlSLoc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlSLoc;
        
        /// <summary>
        /// chkRevolving control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkRevolving;
        
        /// <summary>
        /// chkNonAccural control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkNonAccural;
        
        /// <summary>
        /// chkInDefault control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkInDefault;
        
        /// <summary>
        /// chkStopFin control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkStopFin;
        
        /// <summary>
        /// chkForeclosure control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkForeclosure;
        
        /// <summary>
        /// chkBankruptcy control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkBankruptcy;
        
        /// <summary>
        /// chk203K control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chk203K;
        
        /// <summary>
        /// chkRollToPerm control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkRollToPerm;
        
        /// <summary>
        /// chkAssetManagementt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkAssetManagementt;
        
        /// <summary>
        /// ddlGLTable control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlGLTable;
        
        /// <summary>
        /// ddlStatus control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlStatus;
        
        /// <summary>
        /// ddlFederalCode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlFederalCode;
        
        /// <summary>
        /// ddlLoanGrade control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlLoanGrade;
        
        /// <summary>
        /// txtLoanGrdDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtLoanGrdDate;
        
        /// <summary>
        /// ddlLoanClass control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlLoanClass;
        
        /// <summary>
        /// txtCensusTest control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtCensusTest;
        
        /// <summary>
        /// ddlLoanType control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlLoanType;
        
        /// <summary>
        /// ddlLoanPurpose control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlLoanPurpose;
        
        /// <summary>
        /// ddlCollateralCode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlCollateralCode;
        
        /// <summary>
        /// txtCommitment control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtCommitment;
        
        /// <summary>
        /// tabPnlDates control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlDates;
        
        /// <summary>
        /// txtDateTabApplc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabApplc;
        
        /// <summary>
        /// txtDateTabApprvl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabApprvl;
        
        /// <summary>
        /// txtDateTabClsng control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabClsng;
        
        /// <summary>
        /// txtDateTabPrcntFund control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabPrcntFund;
        
        /// <summary>
        /// txtDateTabCnsStart control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabCnsStart;
        
        /// <summary>
        /// txtDateTabCnsCmpl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabCnsCmpl;
        
        /// <summary>
        /// txtDateTabQotPayOff control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabQotPayOff;
        
        /// <summary>
        /// txtDateTabQotPost control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabQotPost;
        
        /// <summary>
        /// txtDateTabPrssNote control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabPrssNote;
        
        /// <summary>
        /// txtDateTabconvrs control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabconvrs;
        
        /// <summary>
        /// txtDateTabMturty control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabMturty;
        
        /// <summary>
        /// txtDateTabRateLck control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDateTabRateLck;
        
        /// <summary>
        /// tabPnlRelease control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlRelease;
        
        /// <summary>
        /// tabContainerRelease control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer tabContainerRelease;
        
        /// <summary>
        /// tabpnlRlsSch control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabpnlRlsSch;
        
        /// <summary>
        /// txtRlsSchTabNum control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLNumericTextBox txtRlsSchTabNum;
        
        /// <summary>
        /// imgbtnRelsSchAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnRelsSchAdd;
        
        /// <summary>
        /// imgbtnRelsSchEdit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnRelsSchEdit;
        
        /// <summary>
        /// imgbtnRelsSchDel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnRelsSchDel;
        
        /// <summary>
        /// grdRlsSch control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid grdRlsSch;
        
        /// <summary>
        /// hdnItemID control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnItemID;
        
        /// <summary>
        /// tabpnlNotePayOffRules control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabpnlNotePayOffRules;
        
        /// <summary>
        /// chkPayoffShwAll control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkPayoffShwAll;
        
        /// <summary>
        /// cgNotePayOffRules control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid cgNotePayOffRules;
        
        /// <summary>
        /// btnPayoffMoveRight control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnPayoffMoveRight;
        
        /// <summary>
        /// imgbtnNtPayoffRulsDelte control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnNtPayoffRulsDelte;
        
        /// <summary>
        /// imgbtnNotePayOffEdit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnNotePayOffEdit;
        
        /// <summary>
        /// btnNPODelete control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnNPODelete;
        
        /// <summary>
        /// btnNotePayOff control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnNotePayOff;
        
        /// <summary>
        /// tblNotePayOff control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTable tblNotePayOff;
        
        /// <summary>
        /// trSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow trSuccess;
        
        /// <summary>
        /// lblPayOffSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblPayOffSuccess;
        
        /// <summary>
        /// trError control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow trError;
        
        /// <summary>
        /// lblPayOffError control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblPayOffError;
        
        /// <summary>
        /// cgNotPayOffRulsAttach control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid cgNotPayOffRulsAttach;
        
        /// <summary>
        /// btnReleaseHide control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnReleaseHide;
        
        /// <summary>
        /// hdnNotePayOffCount control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnNotePayOffCount;
        
        /// <summary>
        /// tabpnlRules control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabpnlRules;
        
        /// <summary>
        /// chkRlsRulsShwoAll control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkRlsRulsShwoAll;
        
        /// <summary>
        /// drpdwnlstRlsItem control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLDropDownList drpdwnlstRlsItem;
        
        /// <summary>
        /// cstGrdRlsPayoffTemp control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid cstGrdRlsPayoffTemp;
        
        /// <summary>
        /// btnRlsRulesMoveRight control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRlsRulesMoveRight;
        
        /// <summary>
        /// imgbtnReleaseRule control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnReleaseRule;
        
        /// <summary>
        /// imgbtnRelsRulesDel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnRelsRulesDel;
        
        /// <summary>
        /// btnRelsRulesDelete control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRelsRulesDelete;
        
        /// <summary>
        /// btnReleaseRules control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnReleaseRules;
        
        /// <summary>
        /// cstGrdRlsPayoffAtchmnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid cstGrdRlsPayoffAtchmnt;
        
        /// <summary>
        /// tabPnlBdgCntrl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlBdgCntrl;
        
        /// <summary>
        /// ddlBudgets control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlBudgets;
        
        /// <summary>
        /// lblBudgetTitle control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblBudgetTitle;
        
        /// <summary>
        /// imgbtnBdgtCntrlAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnBdgtCntrlAdd;
        
        /// <summary>
        /// imgbtnEdit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnEdit;
        
        /// <summary>
        /// imgbtnBdgtCntrlView control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnBdgtCntrlView;
        
        /// <summary>
        /// ImgbtnDelete control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton ImgbtnDelete;
        
        /// <summary>
        /// imgbtnBdgtCntrlVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnBdgtCntrlVendor;
        
        /// <summary>
        /// btnDeleteBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnDeleteBudget;
        
        /// <summary>
        /// btnSelectBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnSelectBudget;
        
        /// <summary>
        /// hdnBudgetTemp control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnBudgetTemp;
        
        /// <summary>
        /// btnEditBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnEditBudget;
        
        /// <summary>
        /// tblMsgMPopup control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTable tblMsgMPopup;
        
        /// <summary>
        /// trAlertSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow trAlertSuccess;
        
        /// <summary>
        /// lblSuccess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblSuccess;
        
        /// <summary>
        /// ErrorAlert1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow ErrorAlert1;
        
        /// <summary>
        /// lblErrorAlert control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblErrorAlert;
        
        /// <summary>
        /// cgBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid cgBudget;
        
        /// <summary>
        /// ddlInspCompany control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlInspCompany;
        
        /// <summary>
        /// chkOmit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkOmit;
        
        /// <summary>
        /// txtBudgetCommitment control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtBudgetCommitment;
        
        /// <summary>
        /// txtAlctCommit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtAlctCommit;
        
        /// <summary>
        /// txtTotalEstimated control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtTotalEstimated;
        
        /// <summary>
        /// txtTotalAllocated control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtTotalAllocated;
        
        /// <summary>
        /// ddlAutoGenBrwFndFirst control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlAutoGenBrwFndFirst;
        
        /// <summary>
        /// chkOutside control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkOutside;
        
        /// <summary>
        /// hdnBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnBudget;
        
        /// <summary>
        /// tabPnlFinc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlFinc;
        
        /// <summary>
        /// txtFincTabLoanCommit1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLoanCommit1;
        
        /// <summary>
        /// txtFincTabLoanCommit2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLoanCommit2;
        
        /// <summary>
        /// txtGroupId_FilterIndex control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender txtGroupId_FilterIndex;
        
        /// <summary>
        /// txtFincTabLoanCommit3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLoanCommit3;
        
        /// <summary>
        /// FilteredTextBoxExtender1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender1;
        
        /// <summary>
        /// txtFincTabEffctDate1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabEffctDate1;
        
        /// <summary>
        /// drpdwnlstTranscode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList drpdwnlstTranscode;
        
        /// <summary>
        /// lblComRule control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRule;
        
        /// <summary>
        /// drpdwnlstComRule control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList drpdwnlstComRule;
        
        /// <summary>
        /// lblComRulePart0 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRulePart0;
        
        /// <summary>
        /// lblComRulePart1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRulePart1;
        
        /// <summary>
        /// lblComRulePart2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRulePart2;
        
        /// <summary>
        /// lblComRulePart3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRulePart3;
        
        /// <summary>
        /// chkORComRule control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLCheckBox chkORComRule;
        
        /// <summary>
        /// lblComRuleLong control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblComRuleLong;
        
        /// <summary>
        /// pnlPricipal control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlPricipal;
        
        /// <summary>
        /// txtFincTabprincBal1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabprincBal1;
        
        /// <summary>
        /// txtFincTabprincBal2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabprincBal2;
        
        /// <summary>
        /// FilteredTextBoxExtender2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender2;
        
        /// <summary>
        /// txtFincTabprincBal3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabprincBal3;
        
        /// <summary>
        /// FilteredTextBoxExtender3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender3;
        
        /// <summary>
        /// txtFincTabLnLvlDpst1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlDpst1;
        
        /// <summary>
        /// txtFincTabLnLvlDpst2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlDpst2;
        
        /// <summary>
        /// FilteredTextBoxExtender4 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender4;
        
        /// <summary>
        /// txtFincTabLnLvlDpst3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlDpst3;
        
        /// <summary>
        /// FilteredTextBoxExtender5 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender5;
        
        /// <summary>
        /// txtFincTabEffctDate2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabEffctDate2;
        
        /// <summary>
        /// drpdwnlstLnvlDpstEftvTrncode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList drpdwnlstLnvlDpstEftvTrncode;
        
        /// <summary>
        /// txtFincTabLnLvlEscrw1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlEscrw1;
        
        /// <summary>
        /// txtFincTabLnLvlEscrw2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlEscrw2;
        
        /// <summary>
        /// FilteredTextBoxExtender6 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender6;
        
        /// <summary>
        /// txtFincTabLnLvlEscrw3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabLnLvlEscrw3;
        
        /// <summary>
        /// FilteredTextBoxExtender7 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender7;
        
        /// <summary>
        /// txtFincTabEffctDate3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabEffctDate3;
        
        /// <summary>
        /// drpdwnlstLnLvlEscrwTrncode control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList drpdwnlstLnLvlEscrwTrncode;
        
        /// <summary>
        /// txtFincTabOutEqtyCurrnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabOutEqtyCurrnt;
        
        /// <summary>
        /// txtFincTabOutEqtyAdjstmnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabOutEqtyAdjstmnt;
        
        /// <summary>
        /// FilteredTextBoxExtender8 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender8;
        
        /// <summary>
        /// txtFincTabOutEqtyRslt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabOutEqtyRslt;
        
        /// <summary>
        /// FilteredTextBoxExtender9 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender9;
        
        /// <summary>
        /// txtFincTabTotlCurnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabTotlCurnt;
        
        /// <summary>
        /// txtFincTabTotlAdjsmnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabTotlAdjsmnt;
        
        /// <summary>
        /// FilteredTextBoxExtender10 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender10;
        
        /// <summary>
        /// txtFincTabTotlRslt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabTotlRslt;
        
        /// <summary>
        /// FilteredTextBoxExtender11 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender11;
        
        /// <summary>
        /// txtFincTabConstCurrnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabConstCurrnt;
        
        /// <summary>
        /// txtFincTabConstAdjsmnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabConstAdjsmnt;
        
        /// <summary>
        /// FilteredTextBoxExtender12 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender12;
        
        /// <summary>
        /// txtFincTabConstRslt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Web.UI.Controls.TCLTextBox txtFincTabConstRslt;
        
        /// <summary>
        /// FilteredTextBoxExtender13 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender13;
        
        /// <summary>
        /// btnFincTabPostFee control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnFincTabPostFee;
        
        /// <summary>
        /// tabPnlProfiles control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlProfiles;
        
        /// <summary>
        /// tabcontainterProfiles control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer tabcontainterProfiles;
        
        /// <summary>
        /// tabpnlInterestPrfl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabpnlInterestPrfl;
        
        /// <summary>
        /// imgbtnIntrstPrflsAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnIntrstPrflsAdd;
        
        /// <summary>
        /// imgbtnIntrstPrflsDel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnIntrstPrflsDel;
        
        /// <summary>
        /// imgbtnIntrstPrflsCopy control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnIntrstPrflsCopy;
        
        /// <summary>
        /// CGIntrestProfile control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid CGIntrestProfile;
        
        /// <summary>
        /// btnTabIntrstprflTranches control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnTabIntrstprflTranches;
        
        /// <summary>
        /// btnIPTemp control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnIPTemp;
        
        /// <summary>
        /// tabPnlEquityPrfl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlEquityPrfl;
        
        /// <summary>
        /// imgbtEqtyPrflsAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtEqtyPrflsAdd;
        
        /// <summary>
        /// imgbtEqtyPrflsDel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtEqtyPrflsDel;
        
        /// <summary>
        /// imgbtEqtyPrflsCopy control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtEqtyPrflsCopy;
        
        /// <summary>
        /// CGEquityProfile control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid CGEquityProfile;
        
        /// <summary>
        /// btnEPTemp control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnEPTemp;
        
        /// <summary>
        /// tabPnlAtchmnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlAtchmnt;
        
        /// <summary>
        /// tabcontainerAttachemnts control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer tabcontainerAttachemnts;
        
        /// <summary>
        /// tabpnlDocTrack control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabpnlDocTrack;
        
        /// <summary>
        /// lstbStndardArtchBrwDocTrack control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ListBox lstbStndardArtchBrwDocTrack;
        
        /// <summary>
        /// btnDoctMove control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnDoctMove;
        
        /// <summary>
        /// btnDocRemove control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnDocRemove;
        
        /// <summary>
        /// imgbtnDocTracAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnDocTracAdd;
        
        /// <summary>
        /// imgbtnDocTracEdit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnDocTracEdit;
        
        /// <summary>
        /// lstbArtchBrwDocTrack control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ListBox lstbArtchBrwDocTrack;
        
        /// <summary>
        /// tblpnlAttachmets control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tblpnlAttachmets;
        
        /// <summary>
        /// imgbtnAtchmntsAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnAtchmntsAdd;
        
        /// <summary>
        /// imgbtnAtchmntsDel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnAtchmntsDel;
        
        /// <summary>
        /// imgbtnAttachDetails control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnAttachDetails;
        
        /// <summary>
        /// gvAttachments control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid gvAttachments;
        
        /// <summary>
        /// tabPnlBrwBasTerms control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlBrwBasTerms;
        
        /// <summary>
        /// CstGrdBrwBaseTerms control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid CstGrdBrwBaseTerms;
        
        /// <summary>
        /// btnBrwBaseMngTrms control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBrwBaseMngTrms;
        
        /// <summary>
        /// btnRedirectTerms control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRedirectTerms;
        
        /// <summary>
        /// tabPnlBrwBasUnits control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlBrwBasUnits;
        
        /// <summary>
        /// GVUnitTerms control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid GVUnitTerms;
        
        /// <summary>
        /// chkPostInspections control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkPostInspections;
        
        /// <summary>
        /// chkStartPipeline control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkStartPipeline;
        
        /// <summary>
        /// btnBrwBaseFilter control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBrwBaseFilter;
        
        /// <summary>
        /// btnBrwBaseMangUnits control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBrwBaseMangUnits;
        
        /// <summary>
        /// btnRedirectUnits control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRedirectUnits;
        
        /// <summary>
        /// txtAuditLog1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtAuditLog1;
        
        /// <summary>
        /// btnBrwBstabLogUnit1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBrwBstabLogUnit1;
        
        /// <summary>
        /// txtAuditLog2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtAuditLog2;
        
        /// <summary>
        /// btnBrwBstabLogUnit2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBrwBstabLogUnit2;
        
        /// <summary>
        /// ImgAuditAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton ImgAuditAdd;
        
        /// <summary>
        /// ImgAuditDelete control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton ImgAuditDelete;
        
        /// <summary>
        /// hdnAuditDelete control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAuditDelete;
        
        /// <summary>
        /// GVUnitAuditLog control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid GVUnitAuditLog;
        
        /// <summary>
        /// tabPnlkyCnt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabPnlkyCnt;
        
        /// <summary>
        /// btnHideKeyContects control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnHideKeyContects;
        
        /// <summary>
        /// ddlKeyContacts control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlKeyContacts;
        
        /// <summary>
        /// txtFindContact control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtFindContact;
        
        /// <summary>
        /// btnFind control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton btnFind;
        
        /// <summary>
        /// csKeyContacts control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid csKeyContacts;
        
        /// <summary>
        /// pnlKeyContact control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlKeyContact;
        
        /// <summary>
        /// lblRec1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblRec1;
        
        /// <summary>
        /// btnKeyCntsMoveRight control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnKeyCntsMoveRight;
        
        /// <summary>
        /// imgbtnDKeyContact control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnDKeyContact;
        
        /// <summary>
        /// csKeyContactAttached control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid csKeyContactAttached;
        
        /// <summary>
        /// pnlKeyAttached control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlKeyAttached;
        
        /// <summary>
        /// lblRec2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblRec2;
        
        /// <summary>
        /// btnProjectSave control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnProjectSave;
        
        /// <summary>
        /// btnProjectCancel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnProjectCancel;
        
        /// <summary>
        /// upsave control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.UpdatePanel upsave;
        
        /// <summary>
        /// btnSaveProcess control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnSaveProcess;
        
        /// <summary>
        /// hdnfldsPnlUseDfndfld control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldsPnlUseDfndfld;
        
        /// <summary>
        /// hdnfldTntSpcInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldTntSpcInfo;
        
        /// <summary>
        /// hdnfldSlsContractInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldSlsContractInfo;
        
        /// <summary>
        /// hdnfldSalesNewContactInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldSalesNewContactInfo;
        
        /// <summary>
        /// hdnfldTenantNewSpaceNote control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldTenantNewSpaceNote;
        
        /// <summary>
        /// hdnfldTenantSort control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnfldTenantSort;
        
        /// <summary>
        /// hdnVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnVendor;
        
        /// <summary>
        /// hdnRelschUpdate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnRelschUpdate;
        
        /// <summary>
        /// hdnAuditRpt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAuditRpt;
        
        /// <summary>
        /// hdnNonAccrualStatus control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnNonAccrualStatus;
        
        /// <summary>
        /// hdnAprisalInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAprisalInfo;
        
        /// <summary>
        /// hdnNoteNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnNoteNo;
        
        /// <summary>
        /// hdnUnitNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnUnitNo;
        
        /// <summary>
        /// mdlPopupVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mdlPopupVendor;
        
        /// <summary>
        /// mdlpopupiframeuserdefined control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mdlpopupiframeuserdefined;
        
        /// <summary>
        /// mdlPopupRelschUpdate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mdlPopupRelschUpdate;
        
        /// <summary>
        /// MdlPopUpNonAccrualStatus control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender MdlPopUpNonAccrualStatus;
        
        /// <summary>
        /// MdlPopUpAuditRpt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender MdlPopUpAuditRpt;
        
        /// <summary>
        /// PnlUseDfndfld control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel PnlUseDfndfld;
        
        /// <summary>
        /// tagContainerUsrDfndFld control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer tagContainerUsrDfndFld;
        
        /// <summary>
        /// tabAlphaNumFlds control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabAlphaNumFlds;
        
        /// <summary>
        /// text5303 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox text5303;
        
        /// <summary>
        /// text5308 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox text5308;
        
        /// <summary>
        /// text5313 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox text5313;
        
        /// <summary>
        /// tabAmntFlds control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabAmntFlds;
        
        /// <summary>
        /// text5344 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox text5344;
        
        /// <summary>
        /// text5350 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox text5350;
        
        /// <summary>
        /// btn5356 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btn5356;
        
        /// <summary>
        /// btn5357 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btn5357;
        
        /// <summary>
        /// tabDateFlds control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel tabDateFlds;
        
        /// <summary>
        /// txtServicingReleased control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtServicingReleased;
        
        /// <summary>
        /// txtFileAuditDate1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtFileAuditDate1;
        
        /// <summary>
        /// txtFIleAuditDate2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtFIleAuditDate2;
        
        /// <summary>
        /// btnUsrDfnFlsOk control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnUsrDfnFlsOk;
        
        /// <summary>
        /// btnUsrDfnFlsCancel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnUsrDfnFlsCancel;
        
        /// <summary>
        /// pnlVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlVendor;
        
        /// <summary>
        /// lblNoteNumber control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblNoteNumber;
        
        /// <summary>
        /// lblUnit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblUnit;
        
        /// <summary>
        /// txtVNumber control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtVNumber;
        
        /// <summary>
        /// imgbtnSearchVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ImageButton imgbtnSearchVendor;
        
        /// <summary>
        /// lblVName control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblVName;
        
        /// <summary>
        /// lblVAddress1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblVAddress1;
        
        /// <summary>
        /// lblVCity control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblVCity;
        
        /// <summary>
        /// lblVState control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblVState;
        
        /// <summary>
        /// lblVZip control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblVZip;
        
        /// <summary>
        /// egBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid egBudget;
        
        /// <summary>
        /// rbVendorRel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.RadioButtonList rbVendorRel;
        
        /// <summary>
        /// btnApply control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnApply;
        
        /// <summary>
        /// btnCancelVendor control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnCancelVendor;
        
        /// <summary>
        /// pnlRelschUpdate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlRelschUpdate;
        
        /// <summary>
        /// Div1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlGenericControl Div1;
        
        /// <summary>
        /// txtDescription control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDescription;
        
        /// <summary>
        /// chkStatus control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkStatus;
        
        /// <summary>
        /// txtMinimumAmount control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtMinimumAmount;
        
        /// <summary>
        /// txtReleaseDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtReleaseDate;
        
        /// <summary>
        /// txtCurrentRelease control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtCurrentRelease;
        
        /// <summary>
        /// txtLastRelease control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtLastRelease;
        
        /// <summary>
        /// chkPaydownFlag control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkPaydownFlag;
        
        /// <summary>
        /// txtAmtSales control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtAmtSales;
        
        /// <summary>
        /// txtSqFtSales control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtSqFtSales;
        
        /// <summary>
        /// txtPricePerSqFtSales control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPricePerSqFtSales;
        
        /// <summary>
        /// txtAmtAppraisal control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtAmtAppraisal;
        
        /// <summary>
        /// txtSqFtAppraisal control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtSqFtAppraisal;
        
        /// <summary>
        /// txtPricePerSqFtAppraisal control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPricePerSqFtAppraisal;
        
        /// <summary>
        /// txtDiscountedAmt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDiscountedAmt;
        
        /// <summary>
        /// chkType control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.CheckBox chkType;
        
        /// <summary>
        /// txtLastAppDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtLastAppDate;
        
        /// <summary>
        /// txtPctCmp control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPctCmp;
        
        /// <summary>
        /// txtLastInspDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtLastInspDate;
        
        /// <summary>
        /// egPayoffRules control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::ISGN.TCL.Control.CustomGrid.ExtendGrid egPayoffRules;
        
        /// <summary>
        /// btnSaveRelschUpdate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnSaveRelschUpdate;
        
        /// <summary>
        /// btnCancelRelschUpdate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnCancelRelschUpdate;
        
        /// <summary>
        /// pnlNonAccrualStatus control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlNonAccrualStatus;
        
        /// <summary>
        /// txtNonAccrlStatusEffctDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtNonAccrlStatusEffctDate;
        
        /// <summary>
        /// btnNonAccrlStatusYes control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnNonAccrlStatusYes;
        
        /// <summary>
        /// btnNonAccrlStatusNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnNonAccrlStatusNo;
        
        /// <summary>
        /// pnlAuditRpt control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlAuditRpt;
        
        /// <summary>
        /// btnAdtRptYes control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnAdtRptYes;
        
        /// <summary>
        /// btnAdtRptNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnAdtRptNo;
        
        /// <summary>
        /// hdnHide1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnHide1;
        
        /// <summary>
        /// popupLIProfile control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender popupLIProfile;
        
        /// <summary>
        /// pnlLIProfile control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlLIProfile;
        
        /// <summary>
        /// TabContainer1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabContainer TabContainer1;
        
        /// <summary>
        /// TabPanel2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel TabPanel2;
        
        /// <summary>
        /// Button1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button Button1;
        
        /// <summary>
        /// btnCancelLiprofile control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnCancelLiprofile;
        
        /// <summary>
        /// TabPanel3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel TabPanel3;
        
        /// <summary>
        /// btnRoundPnl control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRoundPnl;
        
        /// <summary>
        /// btnLIP2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnLIP2;
        
        /// <summary>
        /// TabPanel4 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.TabPanel TabPanel4;
        
        /// <summary>
        /// btnCancelLIP3 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnCancelLIP3;
        
        /// <summary>
        /// hdnHide2 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnHide2;
        
        /// <summary>
        /// popupRoundOption control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender popupRoundOption;
        
        /// <summary>
        /// PnlRoundOption control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel PnlRoundOption;
        
        /// <summary>
        /// rdRound control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.RadioButtonList rdRound;
        
        /// <summary>
        /// ddlRound control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.DropDownList ddlRound;
        
        /// <summary>
        /// rdRoundOther control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.RadioButton rdRoundOther;
        
        /// <summary>
        /// txtRoundOther control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtRoundOther;
        
        /// <summary>
        /// pnlOther control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlOther;
        
        /// <summary>
        /// lblOther control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblOther;
        
        /// <summary>
        /// pnlGroup control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlGroup;
        
        /// <summary>
        /// lblRate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblRate;
        
        /// <summary>
        /// lblMarign control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblMarign;
        
        /// <summary>
        /// lblRounding control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblRounding;
        
        /// <summary>
        /// btnRoundSave control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnRoundSave;
        
        /// <summary>
        /// btnCancelRound control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnCancelRound;
        
        /// <summary>
        /// hdnIPEffDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnIPEffDate;
        
        /// <summary>
        /// hdnEPEQtype control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnEPEQtype;
        
        /// <summary>
        /// hdnEPEffDate control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnEPEffDate;
        
        /// <summary>
        /// hdnEPBudgetID control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnEPBudgetID;
        
        /// <summary>
        /// hdnAttachDetails control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAttachDetails;
        
        /// <summary>
        /// mPopupAttachdetails control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mPopupAttachdetails;
        
        /// <summary>
        /// pnlAttachDetails control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlAttachDetails;
        
        /// <summary>
        /// lblNoteInfo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblNoteInfo;
        
        /// <summary>
        /// lblAttached control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblAttached;
        
        /// <summary>
        /// lblAttachID control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblAttachID;
        
        /// <summary>
        /// lblDescription control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblDescription;
        
        /// <summary>
        /// btnOk018 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnOk018;
        
        /// <summary>
        /// hdnAttachDoc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAttachDoc;
        
        /// <summary>
        /// mPopupAttachDoc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mPopupAttachDoc;
        
        /// <summary>
        /// docPanel1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.UpdatePanel docPanel1;
        
        /// <summary>
        /// pnlAttachDoc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlAttachDoc;
        
        /// <summary>
        /// trValidsumm control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.HtmlControls.HtmlTableRow trValidsumm;
        
        /// <summary>
        /// ValidationSummaryAttachments control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.ValidationSummary ValidationSummaryAttachments;
        
        /// <summary>
        /// fuAttachments control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.FileUpload fuAttachments;
        
        /// <summary>
        /// reqFlValAttach control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.RequiredFieldValidator reqFlValAttach;
        
        /// <summary>
        /// txtDocument control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDocument;
        
        /// <summary>
        /// btnAttachmentOk control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnAttachmentOk;
        
        /// <summary>
        /// btnAttachmentCancel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnAttachmentCancel;
        
        /// <summary>
        /// hdnAddBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnAddBudget;
        
        /// <summary>
        /// mpeAddBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mpeAddBudget;
        
        /// <summary>
        /// pnlAddBudget control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlAddBudget;
        
        /// <summary>
        /// lblNoteNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblNoteNo;
        
        /// <summary>
        /// lblUnitNumber control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblUnitNumber;
        
        /// <summary>
        /// lblBudgetId control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblBudgetId;
        
        /// <summary>
        /// txtGroupID control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtGroupID;
        
        /// <summary>
        /// txtGroupDesc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtGroupDesc;
        
        /// <summary>
        /// btnAddBudgetOK control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnAddBudgetOK;
        
        /// <summary>
        /// btnBudgetCancel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnBudgetCancel;
        
        /// <summary>
        /// mpopupDocAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.ModalPopupExtender mpopupDocAdd;
        
        /// <summary>
        /// pnlDocAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Panel pnlDocAdd;
        
        /// <summary>
        /// lblDocNoteNo control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblDocNoteNo;
        
        /// <summary>
        /// lblDocUnit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblDocUnit;
        
        /// <summary>
        /// lblDocId control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Label lblDocId;
        
        /// <summary>
        /// txtDocGroupId control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDocGroupId;
        
        /// <summary>
        /// FilteredTextBoxExtender15 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender FilteredTextBoxExtender15;
        
        /// <summary>
        /// txtPri control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtPri;
        
        /// <summary>
        /// txtPri_FilteredTextBoxExtender1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender txtPri_FilteredTextBoxExtender1;
        
        /// <summary>
        /// txtBorDays control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtBorDays;
        
        /// <summary>
        /// txtBorDays_FilteredTextBoxExtender1 control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::AjaxControlToolkit.FilteredTextBoxExtender txtBorDays_FilteredTextBoxExtender1;
        
        /// <summary>
        /// txtDocDesc control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.TextBox txtDocDesc;
        
        /// <summary>
        /// btnDocIdMain control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnDocIdMain;
        
        /// <summary>
        /// btnDocCancel control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.Button btnDocCancel;
        
        /// <summary>
        /// hdnDocEdit control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnDocEdit;
        
        /// <summary>
        /// hdnDocAdd control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnDocAdd;
        
        /// <summary>
        /// hdnDocId control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnDocId;
        
        /// <summary>
        /// hdnInquiry control.
        /// </summary>
        /// <remarks>
        /// Auto-generated field.
        /// To modify move field declaration from designer file to code-behind file.
        /// </remarks>
        protected global::System.Web.UI.WebControls.HiddenField hdnInquiry;
    }
}



Note Info.js




function IsNumericValue(ctrl, evt) {
    var test_result = /^\d+$/.test(ctrl.value);
    var iKeyCode = (evt.which) ? evt.which : evt.keyCode
    if (iKeyCode != 46 && iKeyCode > 31 && (iKeyCode < 48 || iKeyCode > 57)) {
        return false;
    }
    else if (test_result == false) {
        ctrl.value = "";
    }
}
$(document).ready(function () {

    datpick();
    DatePicker();
   // valchkExtendedPwd();

});

function datpick() {
//collapsable panel
 $('#ctl00_Maincontent_TabNoteInfo_tabPnlFinc_pnlLoanlevelHeader').click(function() {
               $('#ctl00_Maincontent_TabNoteInfo_tabPnlFinc_pnlLnLvlDpstContent').slideToggle('slow');
         });
         //collapsable panel
         $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBasUnits_txtAuditLog1").dateEntry();
         $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBasUnits_txtAuditLog1").datepicker({
             constrainInput: true,
             showOn: "button",
             buttonImageOnly: true,
             //                    buttonImageOnly: false,
             buttonImage: "/Images/date-picker-icon.gif",
             changeMonth: true,
             changeYear: true,
             buttonText: "Calendar",
             onSelect: function() {
                 this.fireEvent && this.fireEvent('onchange') || $(this).change();
             }
         });
         $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBasUnits_txtAuditLog2").dateEntry();
         $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBasUnits_txtAuditLog2").datepicker({
             constrainInput: true,
             showOn: "button",
             buttonImageOnly: true,
             //                    buttonImageOnly: false,
             buttonImage: "/Images/date-picker-icon.gif",
             changeMonth: true,
             changeYear: true,
             buttonText: "Calendar",
             onSelect: function() {
                 this.fireEvent && this.fireEvent('onchange') || $(this).change();
             }
         });
    $("#Maincontent_txtNonAccrlStatusEffctDate").dateEntry();
    $("#Maincontent_txtNonAccrlStatusEffctDate").datepicker({
    constrainInput: true,
    showOn: "button",
    buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });


    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtGnrlTabLoanGrdDate").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtGnrlTabLoanGrdDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtGnrlTabCmmit").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtGnrlTabCmmit").datepicker({
    constrainInput: true,
    showOn: "button",
    buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });


    $("#Maincontent_txtSlsNewCntrctDate").dateEntry();
    $("#Maincontent_txtSlsNewCntrctDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#Maincontent_txtSlsNewKickoutDate").dateEntry();
    $("#Maincontent_txtSlsNewKickoutDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtServicingReleased").dateEntry();
    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtServicingReleased").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFileAuditDate1").dateEntry();
    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFileAuditDate1").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").dateEntry();
    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

//    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").dateEntry();
//    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").datepicker({
//        constrainInput: true,

//        //                    buttonImageOnly: false,
//        buttonImage: "/Images/date-picker-icon.gif",
//        changeMonth: true,
//        changeYear: true,
//        buttonText: "Calendar",
//        onSelect: function () {
//            this.fireEvent && this.fireEvent('onchange') || $(this).change();
//        }
//    });
//    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").dateEntry();
//    $("#ctl00_Maincontent_tagContainerUsrDfndFld_tabDateFlds_txtFIleAuditDate2").datepicker({
//        constrainInput: true,

//        //                    buttonImageOnly: false,
//        buttonImage: "/Images/date-picker-icon.gif",
//        changeMonth: true,
//        changeYear: true,
//        buttonText: "Calendar",
//        onSelect: function () {
//            this.fireEvent && this.fireEvent('onchange') || $(this).change();
//        }
//    });




    $("#Maincontent_txtTntNewSpcLeasAgrmnt").dateEntry();
    $("#Maincontent_txtTntNewSpcLeasAgrmnt").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#Maincontent_txtTntNewSpcLeasStart").dateEntry();
    $("#Maincontent_txtTntNewSpcLeasStart").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#Maincontent_txtTntNewSpcLeasEnd").dateEntry();
    $("#Maincontent_txtTntNewSpcLeasEnd").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#Maincontent_txtTntNewSpcCertfdOFOcupy").dateEntry();
    $("#Maincontent_txtTntNewSpcCertfdOFOcupy").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#Maincontent_txtReleaseDate").dateEntry();
    $("#Maincontent_txtReleaseDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });



}
function DatePicker() {
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBas_txtBrwBaseRencon").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBas_txtBrwBaseRencon").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBas_txtBrwBaseAudt").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlBrwBas_txtBrwBaseAudt").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabApplc").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabApplc").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabApprvl").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabApprvl").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabClsng").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabClsng").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabCnsStart").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabCnsStart").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabCnsCmpl").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabCnsCmpl").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPayOff").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPayOff").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPayOff").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPayOff").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPost").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabQotPost").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabPrssNote").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabPrssNote").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabMturty").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabMturty").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabconvrs").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabconvrs").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        //                    buttonImageOnly: false,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabRateLck").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlDates_txtDateTabRateLck").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,      
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function () {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#ctl00_Maincontent_txtLastRelease").dateEntry();
    $("#ctl00_Maincontent_txtLastRelease").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });


    $("#"+FincTabEffctDate3).dateEntry();
    $("#"+FincTabEffctDate3).datepicker({
        constrainInput: true,
        showOn : "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#" + FincTabEffctDate1).dateEntry();
    $("#" + FincTabEffctDate1).datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });

    $("#" + FincTabEffctDate2).dateEntry();
    $("#" + FincTabEffctDate2).datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    
    $("#ctl00_Maincontent_txtReleaseDate").dateEntry();
    $("#ctl00_Maincontent_txtReleaseDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_txtLastAppDate").dateEntry();
    $("#ctl00_Maincontent_txtLastAppDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $("#ctl00_Maincontent_txtLastInspDate").dateEntry();
    $("#ctl00_Maincontent_txtLastInspDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
    $(".btn-slide").click(function() {
        $("#panel").slideToggle("slow");
        $(this).toggleClass("active"); return false;
    });
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtLoanGrdDate").dateEntry();
    $("#ctl00_Maincontent_TabNoteInfo_tabPnlGeneral_txtLoanGrdDate").datepicker({
        constrainInput: true,
        showOn: "button",
        buttonImageOnly: true,
        buttonImage: "/Images/date-picker-icon.gif",
        changeMonth: true,
        changeYear: true,
        buttonText: "Calendar",
        onSelect: function() {
            this.fireEvent && this.fireEvent('onchange') || $(this).change();
        }
    });
}

function removeSpecialCharacter(value) {
    if (value.length > 0) {
        var RetValue = value.replace('$', '');
        return RetValue = RetValue.replace(/,/g, '');
    }
    else {
        return value;
    }
}



    

