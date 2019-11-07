# Utilizzo della libreria ClosedXml per la creazione di file Excel
## Requires
- Visual Studio 2010
## License
- Apache License, Version 2.0
## Technologies
- C#
- Excel
- Windows Forms
- Visual Studio 2010
- Windows SDK
- .NET Framework 4
- .NET Framework
- Microsoft Office Excel 2007
- Visual Basic.NET
- VB.Net
- .NET Framework 4.0
- Excel 2007
- Open XML SDK 2.0
- Windows General
- C# Language
- WinForms
## Topics
- C#
- Excel
- Windows Forms
- Visual Basic .NET
- Visual basic
- VB.Net
- .NET 4
- ClosedXml
- OpenXml
## Updated
- 11/17/2012
## Description

<h1>Introduction</h1>
<p><em>Questo esempio dimostra come utilizzare la libreria ClosedXml.</em></p>
<h1><span>Building the Sample</span></h1>
<p><em>Per poter provare questo esempio occorre avere VisualStudio 2010 , oltre che le libreria ClosedXml.dll e OpenXml di microsoft installato sul proprio pc.</em></p>
<p><span style="font-size:20px; font-weight:bold">Description</span></p>
<p>&nbsp;ClosedXml e un file con estensione .dll pensato per poter creare con estrema facilit&agrave; dei file Excel con pochi e semplici passaggi. Potete trovare tutta la documentazione e scaricare ClosedXml da Codeplex , il link e disponibile qui di seguito
<a href="http://closedxml.codeplex.com/">http://closedxml.codeplex.com/</a>&nbsp;.&nbsp;Con ClosedXml si&nbsp;possono creare file Excel 2007 e versione 2010 , tener conto che per poter utilizzare ClosedXml abbiamo anche bisogno di installare OpenXml di Microsoft
 disponibile per il Download qui di seguito <a href="http://www.microsoft.com/en-us/download/details.aspx?id=5124">
http://www.microsoft.com/en-us/download/details.aspx?id=5124</a>.In questo esempio vi &egrave; un DataBase creato per semplicit&agrave; con SqlCompact , dove e possibile inserire i dati in una tabella chiamata UserData in modo poi da poterli visualizzare in
 anteprima mediante un DataGrid e un form dedicato.Allafine sar&agrave; possibile salvare e visualizzare il risultato mediante un file excel visibile in figura successiva.Qui di seguito riporto anche il codice utilizzato.</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Modifica script</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span><span class="hidden">csharp</span>
<pre class="hidden">'FrmClodedXmlSample
Public Class FrmClosedXmlSample

    'I declare a variable of type bool, this variable is handled when the user 
    'select a row in the DataGrid control to allow you to erase and edit data
    Dim _checkifrowisselected As Boolean

    'FrmClosedXmlSampleLoad event
    Private Sub FrmClosedXmlSampleLoad(sender As System.Object, e As EventArgs) Handles MyBase.Load
        'This method loads the data into the control using the TableAdapter's Fill method,  
        'and then the DataGridView control is enhanced with the original data using the DataSource property
        LoadDataGrid()
    End Sub

    'LoadDataGrid Method
    Private Sub LoadDataGrid()
        'Load the data into the control TableAdapter
        USERDATATableAdapter.Fill(UserDataSet.USERDATA)
        'Load data with the DataGrid control
        dgvUserData.DataSource = USERDATABindingSource
    End Sub

    'BtnEsciClick event
    Private Sub BtnEsciClick(sender As System.Object, e As EventArgs) Handles btnEsci.Click
        'Close application
        Close()
    End Sub

    'BtnNewClick Event
    Private Sub BtnNuovoClick(sender As System.Object, e As EventArgs) Handles btnNuovo.Click
        'Insert this method does nothing but make the exploitation of fields of DataTable after inserting a new record into the table UserData
        USERDATATableAdapter.Insert(txtName.Text.ToUpper(), txtSurname.Text.ToUpper(), txtAddress.Text.ToUpper(), txtTelephoneNumber.Text.ToUpper(),
                                    txtCity.Text.ToUpper(), txtNationality.Text.ToUpper())

        'This method loads the data into the control using the TableAdapter's Fill method,  
        'and then the DataGridView control is enhanced with the original data using the DataSource property
        LoadDataGrid()
    End Sub

    'BtnDeleteClick Event
    Private Sub BtnEliminaClick(sender As System.Object, e As EventArgs) Handles btnElimina.Click
        'If not _checkifrowisselected equals false
        If Not _checkifrowisselected.Equals(False) Then
            'check if current row is not null
            If dgvUserData.CurrentRow Is Nothing Then
                Return
            End If

            'Delete this method does is erase the fields in the UserData table, execute the passing as argument the number of records that we select using the DataGridView control, 
            'before removal of the record, it checks to see if the user has selected or least one row of the DataGridView control
            USERDATATableAdapter.Delete(Integer.Parse(dgvUserData.CurrentRow.Cells(0).Value.ToString()))

            'This method loads the data into the control using the TableAdapter's Fill method, 
            'and then the DataGridView control is enhanced with the original data using the DataSource property
            LoadDataGrid()

            'set to false variable
            _checkifrowisselected = False
        Else
            'Visualize message to user
            MessageBox.Show(My.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row)
        End If
    End Sub

    'BtnUpdate Event
    Private Sub BtnModificaClick(sender As System.Object, e As EventArgs) Handles btnModifica.Click
        'If not _checkifrowisselected equals false
        If Not _checkifrowisselected.Equals(False) Then
            'Check if currentrow of DataGric is not null
            If dgvUserData.CurrentRow Is Nothing Then
                Return
            End If

            USERDATATableAdapter.Update(txtName.Text.ToUpper(), txtSurname.Text.ToUpper(), txtAddress.Text.ToUpper(), txtTelephoneNumber.Text.ToUpper(), txtCity.Text.ToUpper(), txtNationality.Text.ToUpper(), _
             Integer.Parse(dgvUserData.CurrentRow.Cells(0).Value.ToString()))

            'This method loads the data into the control using the TableAdapter's Fill method, 
            'and then the DataGridView control is enhanced with the original data using the DataSource property
            LoadDataGrid()

            'set to false variable
            _checkifrowisselected = False
        Else
            'Visualize message to user
            MessageBox.Show(My.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row)
        End If
    End Sub

    'BtnReportClick Event
    Private Sub BtnReportClick(sender As System.Object, e As EventArgs) Handles btnReport.Click
        'I declare a new instance of the Form Frmeport
        Dim frm = New FrmReport
        'Pass data form dgvUserData to Datagrin in FrmReport
        frm.FrmReport(dgvUserData)
        'I'm seeing the Forms user
        frm.Show()
    End Sub

    'BtnFindClick Event
    Private Sub BtnFindClick(sender As System.Object, e As EventArgs) Handles btnFind.Click
        'I get the currently selected text to the ComboBox control*/
        Dim selecteditems = cbxFind.Text

        'Executing the control of the variable SelectedItems with a Switch construct
        Select Case selecteditems
            'if equals &quot;NAME&quot;
            Case &quot;NAME&quot;
                'I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control
                Dim queryname = UserDataSet.USERDATA.Where(Function(f) f.NAME.StartsWith(txtName.Text.ToUpper)).Select(Function(f) New With {f.NAME _
                                , f.SURNAME, f.ADDRESS, f.TELEPHONE, f.CITY, f.NATIONALITI})
                dgvUserData.DataSource = queryname.ToArray

                'if eqUals &quot;CITY&quot;
            Case &quot;CITY&quot;
                'I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control
                Dim querycity = UserDataSet.USERDATA.Where(Function(f) f.NAME.StartsWith(txtCity.Text.ToUpper)).Select(Function(f) New With {f.NAME _
                                , f.SURNAME, f.ADDRESS, f.TELEPHONE, f.CITY, f.NATIONALITI})
                dgvUserData.DataSource = querycity.ToArray

                'if eqUals &quot;NATIONALITY&quot;
            Case &quot;NATIONALITY&quot;
                'I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control
                Dim querynationality = UserDataSet.USERDATA.Where(Function(f) f.NAME.StartsWith(txtNationality.Text.ToUpper)).Select(Function(f) New With {f.NAME _
                , f.SURNAME, f.ADDRESS, f.TELEPHONE, f.CITY, f.NATIONALITI})
                dgvUserData.DataSource = querynationality.ToArray
        End Select

    End Sub

    'CbxFindSelectedIndexChanged event
    Private Sub CbxFindSelectedIndexChanged(sender As System.Object, e As EventArgs) Handles cbxFind.SelectedIndexChanged
        'I get the currently selected text to the ComboBox control*/
        Dim selecteditems = cbxFind.Text

        'Using a query LinqToObjects reimposed the Enabled property to true for all the text boxes on the form
        For Each c In Controls.OfType(Of TextBox)()
            c.Enabled = True
        Next

        'Executing the control of the variable SelectedItems with a Switch construct
        Select Case selecteditems
            'if equals &quot;NAME&quot;
            Case &quot;NAME&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtName.Name)
                    c.Enabled = False
                Next

                'if equals &quot;SURNAME&quot;
            Case &quot;SURNAME&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtSurname.Name)
                    c.Enabled = False
                Next

                'if equals &quot;ADDRESS&quot;
            Case &quot;ADDRESS&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtAddress.Name)
                    c.Enabled = False
                Next

                'if equals &quot;TELEPHONE&quot;
            Case &quot;TELEPHONENUMBER&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtTelephoneNumber.Name)
                    c.Enabled = False
                Next

                'if eqUals &quot;CITY&quot;
            Case &quot;CITY&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtCity.Name)
                    c.Enabled = False
                Next
                'if eqUals &quot;NATIONALITY&quot;
            Case &quot;NATIONALITY&quot;
                'I run a query linq to objects and imposed enable the property if different from the text box specified
                For Each c In From c1 In Controls.OfType(Of TextBox)() Where Not c1.Name.Equals(txtNationality.Name)
                    c.Enabled = False
                Next
        End Select

    End Sub
End Class</pre>
<pre class="hidden">//dll net framework
using System;
using System.Linq;
using System.Windows.Forms;

//NameSpace ClosedXlmSample
namespace ClosedXmlSample
{
    //FrmClosedXml Class
    public partial class FrmClosedXmlSample : Form
    {
        /*I declare a variable of type bool, this variable is handled when the user
         *select a row in the DataGrid control to allow you to erase and edit data*/
        private bool _checkifrowisselected ;
        
        // Constructor of the class FrmClosedXmlSample
        public FrmClosedXmlSample()
        {
            //InitializeComponent Method
            InitializeComponent();
        }

        //FrmClosedXmlSampleLoad Event
        private void FrmClosedXmlSampleLoad(object sender, EventArgs e)
        {
            /*This method loads the data into the control using the TableAdapter's Fill method, 
            and then the DataGridView control is enhanced with the original data using the DataSource property*/
            LoadDataGrid();
        }

        //BtnNewClick Event
        private void BtnNewClick(object sender, EventArgs e)
        {
            /*Insert this method does nothing but make the exploitation of fields of DataTable after inserting a new record into the table UserData*/
            uSERDATATableAdapter.Insert(txtName.Text.ToUpper(), txtSurname.Text.ToUpper(), txtAddress.Text.ToUpper(), txtTelephoneNumber.Text.ToUpper(),
                                        txtCity.Text.ToUpper(), txtNationality.Text.ToUpper());
            
            /*This method loads the data into the control using the TableAdapter's Fill method, 
            and then the DataGridView control is enhanced with the original data using the DataSource property*/
            LoadDataGrid();
        }

        //BtnDeleteClick Event
        private void BtnDeleteClick(object sender, EventArgs e)
        {
            /*If not _checkifrowisselected equals false*/
            if(!_checkifrowisselected.Equals(false))
            {
                /*check if current row is not null*/
                if (dgvUserData.CurrentRow == null) return;

                /*Delete this method does is erase the fields in the UserData table, execute the passing as argument the number of records that we select using the DataGridView control, 
                 *before removal of the record, it checks to see if the user has selected or least one row of the DataGridView control*/
                uSERDATATableAdapter.Delete(int.Parse(dgvUserData.CurrentRow.Cells[0].Value.ToString()));

                /*This method loads the data into the control using the TableAdapter's Fill method, 
                and then the DataGridView control is enhanced with the original data using the DataSource property*/
                LoadDataGrid();

                /*set to false variable*/
                _checkifrowisselected = false;
            }

            else
            {
                /*Visualize message to user*/
                MessageBox.Show(Properties.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row);
            }
        }

        //BtnUpdate Event
        private void BtnUpdateClick(object sender, EventArgs e)
        {
            /*If not _checkifrowisselected equals false*/
            if (!_checkifrowisselected.Equals(false))
            {

                /*Check if currentrow of DataGric is not null*/
                if (dgvUserData.CurrentRow == null) return;

                uSERDATATableAdapter.Update(txtName.Text.ToUpper(), txtSurname.Text.ToUpper(), txtAddress.Text.ToUpper(),
                                            txtTelephoneNumber.Text.ToUpper(),
                                            txtCity.Text.ToUpper(), txtNationality.Text.ToUpper(),
                                            int.Parse(dgvUserData.CurrentRow.Cells[0].Value.ToString()));

                /*This method loads the data into the control using the TableAdapter's Fill method, 
                    and then the DataGridView control is enhanced with the original data using the DataSource property*/
                LoadDataGrid();

                /*set to false variable*/
                _checkifrowisselected = false;
            }

            else
            {
                /*Visualize message to user*/
                MessageBox.Show(Properties.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row);
            }
        }

        //BtnReportClick Event
        private void BtnReportClick(object sender, EventArgs e)
        {
            /*I declare a new instance of the Form Frmeport*/
            var frm = new FrmReport {DataReport = dgvUserData};
            /*I'm seeing the Forms user*/
            frm.Show();
        }

        //BtnExitClick Event
        private void BtnExitClick(object sender, EventArgs e)
        {
            //Close the application and Exit
            Close();
        }

        //BtnFindClick Event
        private void BtnFindClick(object sender, EventArgs e)
        {
            /*I get the currently selected text to the ComboBox control*/
            var selecteditems = cbxFind.Text;

            /*Executing the control of the variable SelectedItems with a Switch construct*/
            switch(selecteditems)
            {
                /*If SelectedItems equals NAME*/
                case &quot;NAME&quot;:
                    /*I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control*/
                    var queryname =
                        userDataSet.USERDATA.Where(w =&gt; w.NAME.StartsWith(txtName.Text.ToUpper())).Select(
                            s =&gt; new {s.NAME, s.SURNAME, s.ADDRESS, s.TELEPHONE, s.CITY, s.NATIONALITI}).OrderBy(o=&gt; o.NAME);
                    dgvUserData.DataSource = queryname.ToArray();
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals CITY*/
                case &quot;CITY&quot;:
                    /*I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control*/
                    var querycity =
                        userDataSet.USERDATA.Where(w=&gt; w.CITY.StartsWith(txtCity.Text.ToUpper())).Select(
                            s =&gt; new { s.NAME, s.SURNAME, s.ADDRESS, s.TELEPHONE, s.CITY, s.NATIONALITI }).OrderBy(o =&gt; o.CITY);
                    dgvUserData.DataSource = querycity.ToArray();
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals NATIONALITY*/
                case &quot;NATIONALITY&quot;:
                    /*I run a query LinqToDataSet with extension method and recover all data from the UserData table and visualize the DataGrid control*/
                    var querynationality =
                        userDataSet.USERDATA.Where(w =&gt; w.NATIONALITI.StartsWith(txtNationality.Text.ToUpper())).Select(
                            s =&gt; new { s.NAME, s.SURNAME, s.ADDRESS, s.TELEPHONE, s.CITY, s.NATIONALITI }).OrderBy(o =&gt; o.NATIONALITI);
                    dgvUserData.DataSource = querynationality.ToArray();
                    /*Exit switch*/
                    break;
            }
        }

        /*LoadDataGrid Method*/
        private void LoadDataGrid()
        {
            /*Load the data into the control TableAdapter*/
            uSERDATATableAdapter.Fill(userDataSet.USERDATA);
            /*Load data with the DataGrid control*/
            dgvUserData.DataSource = uSERDATABindingSource;
        }

        /*CbxFindSelectedIndexChanged Event*/
        private void CbxFindSelectedIndexChanged(object sender, EventArgs e)
        {
            /*I get the currently selected text to the ComboBox control*/
            var selecteditems = cbxFind.Text;

            /*Using a query LinqToObjects reimposed the Enabled property to true for all the text boxes on the form*/
            Controls.OfType&lt;TextBox&gt;().ToList().ForEach(f =&gt; f.Enabled = true);

            /*Executing the control of the variable SelectedItems with a Switch construct*/
            switch (selecteditems)
            {
                /*If SelectedItems equals NAME*/
                case &quot;NAME&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtName&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals SURNAME*/
                case &quot;SURNAME&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtSurname&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals ADDRESS*/
                case &quot;ADDRESS&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtAddress&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals TELEPHONENUMBER*/
                case &quot;TELEPHONENUMBER&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtTelephoneNumber&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /**/
                    break;

                /*If SelectedItems equals CITY*/
                case &quot;CITY&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtCity&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /*Exit switch*/
                    break;

                /*If SelectedItems equals NATIONALITY*/
                case &quot;NATIONALITY&quot;:
                    /*I run a query linq to objects and imposed enable the property if different from the text box specified*/
                    Controls.OfType&lt;TextBox&gt;().Where(w =&gt; !w.Name.Equals(&quot;txtNationality&quot;)).ToList().ForEach(
                        f =&gt; f.Enabled = false);
                    /*Exit switch*/
                    break;
            }
        }

        //DgvUserDataRowHeaderMouseClick Event
        private void DgvUserDataRowHeaderMouseClick(object sender, DataGridViewCellMouseEventArgs e)
        {
            /*set the variable to true */
            _checkifrowisselected = true;
        }
    }
}
</pre>
<div class="preview">
<pre class="vb"><span class="visualBasic__com">'FrmClodedXmlSample</span>&nbsp;
<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;FrmClosedXmlSample&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;declare&nbsp;a&nbsp;variable&nbsp;of&nbsp;type&nbsp;bool,&nbsp;this&nbsp;variable&nbsp;is&nbsp;handled&nbsp;when&nbsp;the&nbsp;user&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'select&nbsp;a&nbsp;row&nbsp;in&nbsp;the&nbsp;DataGrid&nbsp;control&nbsp;to&nbsp;allow&nbsp;you&nbsp;to&nbsp;erase&nbsp;and&nbsp;edit&nbsp;data</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;_checkifrowisselected&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Boolean</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'FrmClosedXmlSampleLoad&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;FrmClosedXmlSampleLoad(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;<span class="visualBasic__keyword">MyBase</span>.Load&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;loads&nbsp;the&nbsp;data&nbsp;into&nbsp;the&nbsp;control&nbsp;using&nbsp;the&nbsp;TableAdapter's&nbsp;Fill&nbsp;method,&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'and&nbsp;then&nbsp;the&nbsp;DataGridView&nbsp;control&nbsp;is&nbsp;enhanced&nbsp;with&nbsp;the&nbsp;original&nbsp;data&nbsp;using&nbsp;the&nbsp;DataSource&nbsp;property</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;LoadDataGrid()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'LoadDataGrid&nbsp;Method</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;LoadDataGrid()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Load&nbsp;the&nbsp;data&nbsp;into&nbsp;the&nbsp;control&nbsp;TableAdapter</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USERDATATableAdapter.Fill(UserDataSet.USERDATA)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Load&nbsp;data&nbsp;with&nbsp;the&nbsp;DataGrid&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dgvUserData.DataSource&nbsp;=&nbsp;USERDATABindingSource&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnEsciClick&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnEsciClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnEsci.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Close&nbsp;application</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Close()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnNewClick&nbsp;Event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnNuovoClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnNuovo.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Insert&nbsp;this&nbsp;method&nbsp;does&nbsp;nothing&nbsp;but&nbsp;make&nbsp;the&nbsp;exploitation&nbsp;of&nbsp;fields&nbsp;of&nbsp;DataTable&nbsp;after&nbsp;inserting&nbsp;a&nbsp;new&nbsp;record&nbsp;into&nbsp;the&nbsp;table&nbsp;UserData</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USERDATATableAdapter.Insert(txtName.Text.ToUpper(),&nbsp;txtSurname.Text.ToUpper(),&nbsp;txtAddress.Text.ToUpper(),&nbsp;txtTelephoneNumber.Text.ToUpper(),&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txtCity.Text.ToUpper(),&nbsp;txtNationality.Text.ToUpper())&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;loads&nbsp;the&nbsp;data&nbsp;into&nbsp;the&nbsp;control&nbsp;using&nbsp;the&nbsp;TableAdapter's&nbsp;Fill&nbsp;method,&nbsp;&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'and&nbsp;then&nbsp;the&nbsp;DataGridView&nbsp;control&nbsp;is&nbsp;enhanced&nbsp;with&nbsp;the&nbsp;original&nbsp;data&nbsp;using&nbsp;the&nbsp;DataSource&nbsp;property</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;LoadDataGrid()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnDeleteClick&nbsp;Event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnEliminaClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnElimina.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;not&nbsp;_checkifrowisselected&nbsp;equals&nbsp;false</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;_checkifrowisselected.Equals(<span class="visualBasic__keyword">False</span>)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'check&nbsp;if&nbsp;current&nbsp;row&nbsp;is&nbsp;not&nbsp;null</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;dgvUserData.CurrentRow&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Return</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Delete&nbsp;this&nbsp;method&nbsp;does&nbsp;is&nbsp;erase&nbsp;the&nbsp;fields&nbsp;in&nbsp;the&nbsp;UserData&nbsp;table,&nbsp;execute&nbsp;the&nbsp;passing&nbsp;as&nbsp;argument&nbsp;the&nbsp;number&nbsp;of&nbsp;records&nbsp;that&nbsp;we&nbsp;select&nbsp;using&nbsp;the&nbsp;DataGridView&nbsp;control,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'before&nbsp;removal&nbsp;of&nbsp;the&nbsp;record,&nbsp;it&nbsp;checks&nbsp;to&nbsp;see&nbsp;if&nbsp;the&nbsp;user&nbsp;has&nbsp;selected&nbsp;or&nbsp;least&nbsp;one&nbsp;row&nbsp;of&nbsp;the&nbsp;DataGridView&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USERDATATableAdapter.Delete(<span class="visualBasic__keyword">Integer</span>.Parse(dgvUserData.CurrentRow.Cells(<span class="visualBasic__number">0</span>).Value.ToString()))&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;loads&nbsp;the&nbsp;data&nbsp;into&nbsp;the&nbsp;control&nbsp;using&nbsp;the&nbsp;TableAdapter's&nbsp;Fill&nbsp;method,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'and&nbsp;then&nbsp;the&nbsp;DataGridView&nbsp;control&nbsp;is&nbsp;enhanced&nbsp;with&nbsp;the&nbsp;original&nbsp;data&nbsp;using&nbsp;the&nbsp;DataSource&nbsp;property</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;LoadDataGrid()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'set&nbsp;to&nbsp;false&nbsp;variable</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_checkifrowisselected&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Visualize&nbsp;message&nbsp;to&nbsp;user</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MessageBox.Show(My.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnUpdate&nbsp;Event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnModificaClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnModifica.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;not&nbsp;_checkifrowisselected&nbsp;equals&nbsp;false</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;_checkifrowisselected.Equals(<span class="visualBasic__keyword">False</span>)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Check&nbsp;if&nbsp;currentrow&nbsp;of&nbsp;DataGric&nbsp;is&nbsp;not&nbsp;null</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;dgvUserData.CurrentRow&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Return</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USERDATATableAdapter.Update(txtName.Text.ToUpper(),&nbsp;txtSurname.Text.ToUpper(),&nbsp;txtAddress.Text.ToUpper(),&nbsp;txtTelephoneNumber.Text.ToUpper(),&nbsp;txtCity.Text.ToUpper(),&nbsp;txtNationality.Text.ToUpper(),&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Integer</span>.Parse(dgvUserData.CurrentRow.Cells(<span class="visualBasic__number">0</span>).Value.ToString()))&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;loads&nbsp;the&nbsp;data&nbsp;into&nbsp;the&nbsp;control&nbsp;using&nbsp;the&nbsp;TableAdapter's&nbsp;Fill&nbsp;method,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'and&nbsp;then&nbsp;the&nbsp;DataGridView&nbsp;control&nbsp;is&nbsp;enhanced&nbsp;with&nbsp;the&nbsp;original&nbsp;data&nbsp;using&nbsp;the&nbsp;DataSource&nbsp;property</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;LoadDataGrid()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'set&nbsp;to&nbsp;false&nbsp;variable</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_checkifrowisselected&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Visualize&nbsp;message&nbsp;to&nbsp;user</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MessageBox.Show(My.Resources.FrmClosedXmlSample_BtnDeleteClick_Select_one_row)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnReportClick&nbsp;Event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnReportClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnReport.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;declare&nbsp;a&nbsp;new&nbsp;instance&nbsp;of&nbsp;the&nbsp;Form&nbsp;Frmeport</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;frm&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;FrmReport&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Pass&nbsp;data&nbsp;form&nbsp;dgvUserData&nbsp;to&nbsp;Datagrin&nbsp;in&nbsp;FrmReport</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;frm.FrmReport(dgvUserData)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I'm&nbsp;seeing&nbsp;the&nbsp;Forms&nbsp;user</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;frm.Show()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnFindClick&nbsp;Event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnFindClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnFind.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;get&nbsp;the&nbsp;currently&nbsp;selected&nbsp;text&nbsp;to&nbsp;the&nbsp;ComboBox&nbsp;control*/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;selecteditems&nbsp;=&nbsp;cbxFind.Text&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Executing&nbsp;the&nbsp;control&nbsp;of&nbsp;the&nbsp;variable&nbsp;SelectedItems&nbsp;with&nbsp;a&nbsp;Switch&nbsp;construct</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Select</span>&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;selecteditems&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;equals&nbsp;&quot;NAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;NAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;LinqToDataSet&nbsp;with&nbsp;extension&nbsp;method&nbsp;and&nbsp;recover&nbsp;all&nbsp;data&nbsp;from&nbsp;the&nbsp;UserData&nbsp;table&nbsp;and&nbsp;visualize&nbsp;the&nbsp;DataGrid&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;queryname&nbsp;=&nbsp;UserDataSet.USERDATA.Where(<span class="visualBasic__keyword">Function</span>(f)&nbsp;f.NAME.StartsWith(txtName.Text.ToUpper)).<span class="visualBasic__keyword">Select</span>(<span class="visualBasic__keyword">Function</span>(f)&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;{f.NAME&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;,&nbsp;f.SURNAME,&nbsp;f.ADDRESS,&nbsp;f.TELEPHONE,&nbsp;f.CITY,&nbsp;f.NATIONALITI})&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dgvUserData.DataSource&nbsp;=&nbsp;queryname.ToArray&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;eqUals&nbsp;&quot;CITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;CITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;LinqToDataSet&nbsp;with&nbsp;extension&nbsp;method&nbsp;and&nbsp;recover&nbsp;all&nbsp;data&nbsp;from&nbsp;the&nbsp;UserData&nbsp;table&nbsp;and&nbsp;visualize&nbsp;the&nbsp;DataGrid&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;querycity&nbsp;=&nbsp;UserDataSet.USERDATA.Where(<span class="visualBasic__keyword">Function</span>(f)&nbsp;f.NAME.StartsWith(txtCity.Text.ToUpper)).<span class="visualBasic__keyword">Select</span>(<span class="visualBasic__keyword">Function</span>(f)&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;{f.NAME&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;,&nbsp;f.SURNAME,&nbsp;f.ADDRESS,&nbsp;f.TELEPHONE,&nbsp;f.CITY,&nbsp;f.NATIONALITI})&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dgvUserData.DataSource&nbsp;=&nbsp;querycity.ToArray&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;eqUals&nbsp;&quot;NATIONALITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;NATIONALITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;LinqToDataSet&nbsp;with&nbsp;extension&nbsp;method&nbsp;and&nbsp;recover&nbsp;all&nbsp;data&nbsp;from&nbsp;the&nbsp;UserData&nbsp;table&nbsp;and&nbsp;visualize&nbsp;the&nbsp;DataGrid&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;querynationality&nbsp;=&nbsp;UserDataSet.USERDATA.Where(<span class="visualBasic__keyword">Function</span>(f)&nbsp;f.NAME.StartsWith(txtNationality.Text.ToUpper)).<span class="visualBasic__keyword">Select</span>(<span class="visualBasic__keyword">Function</span>(f)&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;{f.NAME&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;,&nbsp;f.SURNAME,&nbsp;f.ADDRESS,&nbsp;f.TELEPHONE,&nbsp;f.CITY,&nbsp;f.NATIONALITI})&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dgvUserData.DataSource&nbsp;=&nbsp;querynationality.ToArray&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Select</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'CbxFindSelectedIndexChanged&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;CbxFindSelectedIndexChanged(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;cbxFind.SelectedIndexChanged&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;get&nbsp;the&nbsp;currently&nbsp;selected&nbsp;text&nbsp;to&nbsp;the&nbsp;ComboBox&nbsp;control*/</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;selecteditems&nbsp;=&nbsp;cbxFind.Text&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Using&nbsp;a&nbsp;query&nbsp;LinqToObjects&nbsp;reimposed&nbsp;the&nbsp;Enabled&nbsp;property&nbsp;to&nbsp;true&nbsp;for&nbsp;all&nbsp;the&nbsp;text&nbsp;boxes&nbsp;on&nbsp;the&nbsp;form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">True</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Executing&nbsp;the&nbsp;control&nbsp;of&nbsp;the&nbsp;variable&nbsp;SelectedItems&nbsp;with&nbsp;a&nbsp;Switch&nbsp;construct</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Select</span>&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;selecteditems&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;equals&nbsp;&quot;NAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;NAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtName.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;equals&nbsp;&quot;SURNAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;SURNAME&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtSurname.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;equals&nbsp;&quot;ADDRESS&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;ADDRESS&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtAddress.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;equals&nbsp;&quot;TELEPHONE&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;TELEPHONENUMBER&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtTelephoneNumber.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;eqUals&nbsp;&quot;CITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;CITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtCity.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'if&nbsp;eqUals&nbsp;&quot;NATIONALITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Case</span>&nbsp;<span class="visualBasic__string">&quot;NATIONALITY&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;run&nbsp;a&nbsp;query&nbsp;linq&nbsp;to&nbsp;objects&nbsp;and&nbsp;imposed&nbsp;enable&nbsp;the&nbsp;property&nbsp;if&nbsp;different&nbsp;from&nbsp;the&nbsp;text&nbsp;box&nbsp;specified</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;<span class="visualBasic__keyword">Each</span>&nbsp;c&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;From&nbsp;c1&nbsp;<span class="visualBasic__keyword">In</span>&nbsp;Controls.OfType(<span class="visualBasic__keyword">Of</span>&nbsp;TextBox)()&nbsp;Where&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;c1.Name.Equals(txtNationality.Name)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c.Enabled&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Select</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Class</span></pre>
</div>
</div>
</div>
<div class="scriptcode">Questa era la parte di codice per l'interazione con i dati , quindi solo L'insert , il Delete e Update, di seguito tutto il codice per creare un file excel.</div>
<div class="scriptcode">
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Modifica script</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span><span class="hidden">csharp</span>
<pre class="hidden">'dll netFramework
Imports System.Globalization
Imports ClosedXML.Excel

'FrmReport Class
Public Class FrmReport

    'Sub FrmReport
    Public Sub FrmReport(ByVal datareport As DataGridView)
        'Enhanced the value control DataGrid using the property DataReport
        dgvReport.DataSource = datareport.DataSource
    End Sub

    'BtnExitClick event
    Private Sub BtnExitClick(sender As System.Object, e As EventArgs) Handles btnExit.Click
        'Close actual Form
        Close()
    End Sub

    'BtnExportToExcelClick event
    Private Sub BtnExportToExcelClick(sender As System.Object, e As EventArgs) Handles btnExportToExcel.Click
        'If the DataGrid control does not contain any column
        If dgvReport.Columns.Count.Equals(0) Then
            'I get a message to the user
            MessageBox.Show(My.Resources.FrmReport_BtnSalvaInExcelClick_Nessuna_riga_da_salvare, Application.ProductName.ToString(CultureInfo.InvariantCulture))
            Return
        End If

        'Imposed on the size of the file to be saved for the SaveFileDialog component, 
        'the format and saved in the application's resources.
        sfDialog.Filter = My.Resources.FileXlsx

        'Given the name of the excel file that will be generated.
        sfDialog.FileName = &quot;USER DATA&quot;

        'Here, however, we create a new worksheet excel
        Dim workbook = New XLWorkbook()

        'On the worksheet, create the worksheet in another sheet named user reports, 
        'this leaflet will be included in the excel file which will then be generated.
        Dim worksheet = workbook.Worksheets.Add(&quot;USER DATA REPORT&quot;)

        'I create variables as there are columns of excel file to be created, 
        'in this case 6 and the imposed with a default value
        Dim cellA = &quot;A&quot;
        Dim cellB = &quot;B&quot;
        Dim cellC = &quot;C&quot;
        Dim cellD = &quot;D&quot;
        Dim cellE = &quot;E&quot;
        Dim cellF = &quot;F&quot;

        'This variable is used for the process of writing the various sections of the paper, the header, 
        'the name of the columns to end up with the values ​​of the DataGrid control
        Dim indexcell = 0

        'In this loop we perform the control of the variable index and it will create the header of the sheet, 
        'a title and the formatting of cells on the alignment of the title text
        For riga = 0 To 3
            'In this loop are enclosed in stages to the header in the title, the cell formatting and the column headings
            indexcell &#43;= 1

            'If index equals 1
            If indexcell.Equals(1) Then
                'Allowance for cells and and the numerical value given by the variable i and indexcell
                cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture)

                'The Merge method allows to combine two or more cells, in this case we combine the cells from a to f
                worksheet.Range(cellA &#43; &quot;:&quot; &#43; cellF).Merge()

                'Assign a value to the cell, so that it can fill the contents of the cells to f
                worksheet.Cell(cellA).Value = &quot;USER DATA&quot;

                'Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center
                worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellA).Style.Fill.BackgroundColor = XLColor.CornflowerBlue

                'default value for cell a and f
                cellA = &quot;A&quot;
                cellF = &quot;F&quot;
            End If

            'If index equals 2
            If indexcell.Equals(2) Then
                'Allowance for cells and and the numerical value given by the variable i and indexcell
                cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellB &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellC &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellD &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellE &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture)

                'Here, however, we assign the cell to the cell f the name of the columns of the DataGrid control by property Value
                worksheet.Cell(cellA).Value = dgvReport.Columns(1).Name
                worksheet.Cell(cellB).Value = dgvReport.Columns(2).Name
                worksheet.Cell(cellC).Value = dgvReport.Columns(3).Name
                worksheet.Cell(cellD).Value = dgvReport.Columns(4).Name
                worksheet.Cell(cellE).Value = dgvReport.Columns(5).Name
                worksheet.Cell(cellF).Value = dgvReport.Columns(6).Name

                'Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center
                worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellB).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellC).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellD).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellE).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellF).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center

                'default value for cell from a to f
                cellA = &quot;A&quot;
                cellB = &quot;B&quot;
                cellC = &quot;C&quot;
                cellD = &quot;D&quot;
                cellE = &quot;E&quot;
                cellF = &quot;F&quot;
            End If
        Next

        'In this loop will perform the control of the variable index and prodceder&agrave; to the writing of the values ​​contained in 
        'the DataGrid on the variables from cell to celfl, so pore actually write on the cells of the sheet excel
        For riga = 0 To dgvReport.Rows.Count - 1
            'If index equals 3
            If indexcell &gt; 3 Then
                'Allowance for cells and and the numerical value given by the variable i and indexcell
                cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellB &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellC &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellD &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellE &#43;= indexcell.ToString(CultureInfo.InvariantCulture)
                cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture)

                'Here instead we assign from cell to cell f the value of each row in the DataGrid control and always through their Value property
                worksheet.Cell(cellA).Value = dgvReport.Rows(riga).Cells(1).Value
                worksheet.Cell(cellB).Value = dgvReport.Rows(riga).Cells(2).Value
                worksheet.Cell(cellC).Value = dgvReport.Rows(riga).Cells(3).Value
                worksheet.Cell(cellD).Value = dgvReport.Rows(riga).Cells(4).Value
                worksheet.Cell(cellE).Value = dgvReport.Rows(riga).Cells(5).Value
                worksheet.Cell(cellF).Value = dgvReport.Rows(riga).Cells(6).Value

                'Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center
                worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellB).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellC).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellD).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellE).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center
                worksheet.Cell(cellF).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center

                'This method allows to adapt the text within the cells so that it is well centered and adapted to their inner
                worksheet.Columns().AdjustToContents()

                'default value for cell from a to f
                cellA = &quot;A&quot;
                cellB = &quot;B&quot;
                cellC = &quot;C&quot;
                cellD = &quot;D&quot;
                cellE = &quot;E&quot;
                cellF = &quot;F&quot;
            End If

            'increase the value of the variable indexcell
            indexcell &#43;= 1
        Next

        'Here we give the user the possibility scegiere where to save the file which will then be generated using the SaveFileDialog
        If sfDialog.ShowDialog().Equals(DialogResult.OK) Then
            'This method will save the file in xlsx excel where the user decide this 
            'by the argument required by that method where we spend the path of destination
            workbook.SaveAs(sfDialog.FileName)
        End If
    End Sub
End Class
</pre>
<pre class="hidden">//dll net framework
using System;
using System.Globalization;
using System.Windows.Forms;
using ClosedXmlSample.Properties;

//This and instead the reference that must be included in the project to use the library ClosedXml
using ClosedXML.Excel;

//NameSpace ClosedXlmSample
namespace ClosedXmlSample
{
    //FrmReport Class
    public partial class FrmReport : Form
    {
        // Constructor of the class FrmReport
        public FrmReport()
        {
            //InitializeComponent Method
            InitializeComponent();
        }

        //This property is value in the main form with the values ​​in the DataGrid, which then in turn enhances the Forms DataGrid control FrmReport
        public DataGridView DataReport { get; set; }

        //FrmReportLoad Event
        private void FrmReportLoad(object sender, EventArgs e)
        {
            /*Enhanced the value control DataGrid using the property DataReport*/
            dgvReport.DataSource = DataReport.DataSource;
        }

        //BtnExportToExcelClick Event
        private void BtnExportToExcelClick(object sender, EventArgs e)
        {
            /*If the DataGrid control does not contain any column*/
            if (dgvReport.Columns.Count.Equals(0))
            {
                /*I get a message to the user*/
                MessageBox.Show(Resources.FrmReport_BtnSalvaInExcelClick_Nessuna_riga_da_salvare, Application.ProductName.ToString(CultureInfo.InvariantCulture));
                return;
            }

            /*Imposed on the size of the file to be saved for the SaveFileDialog component, 
             * the format and saved in the application's resources.*/
            sfDialog.Filter = Resources.FileXlsx;

            /*Given the name of the excel file that will be generated.*/
            sfDialog.FileName = &quot;USER DATA&quot;;

            /*Here, however, we create a new worksheet excel*/
            var workbook = new XLWorkbook();

            /*On the worksheet, create the worksheet in another sheet named user reports, 
             * this leaflet will be included in the excel file which will then be generated.*/
            var worksheet = workbook.Worksheets.Add(&quot;USER DATA REPORT&quot;);

            /*I create variables as there are columns of excel file to be created, 
             * in this case 6 and the imposed with a default value*/
            var cellA = &quot;A&quot;;
            var cellB = &quot;B&quot;;
            var cellC = &quot;C&quot;;
            var cellD = &quot;D&quot;;
            var cellE = &quot;E&quot;;
            var cellF = &quot;F&quot;;

            /*This variable is used for the process of writing the various sections of the paper, the header, 
             * the name of the columns to end up with the values ​​of the DataGrid control*/
            var indexcell = 0;

            /*In this loop we perform the control of the variable index and it will create the header of the sheet, 
             * a title and the formatting of cells on the alignment of the title text*/
            for (var riga = 0; riga &lt; 4; riga&#43;&#43;)
            {
                /*In this loop are enclosed in stages to the header in the title, the cell formatting and the column headings*/
                indexcell &#43;= 1;

                /*If index equals 1*/
                if (indexcell.Equals(1))
                {
                    /*Allowance for cells and and the numerical value given by the variable i and indexcell*/
                    cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture);

                    /*The Merge method allows to combine two or more cells, in this case we combine the cells from a to f*/
                    worksheet.Range(cellA &#43; &quot;:&quot; &#43; cellF).Merge();

                    /*Assign a value to the cell, so that it can fill the contents of the cells to f*/
                    worksheet.Cell(cellA).Value = &quot;USER DATA&quot;;

                    /*Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center*/
                    worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellA).Style.Fill.BackgroundColor = XLColor.CornflowerBlue;

                    /*default value for cell a and f*/
                    cellA = &quot;A&quot;;
                    cellF = &quot;F&quot;;
                }

                /*If index equals 2*/
                if (indexcell.Equals(2))
                {
                    /*Allowance for cells and and the numerical value given by the variable i and indexcell*/
                    cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellB &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellC &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellD &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellE &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture);

                    /*Here, however, we assign the cell to the cell f the name of the columns of the DataGrid control by property Value*/
                    worksheet.Cell(cellA).Value = dgvReport.Columns[1].Name;
                    worksheet.Cell(cellB).Value = dgvReport.Columns[2].Name;
                    worksheet.Cell(cellC).Value = dgvReport.Columns[3].Name;
                    worksheet.Cell(cellD).Value = dgvReport.Columns[4].Name;
                    worksheet.Cell(cellE).Value = dgvReport.Columns[5].Name;
                    worksheet.Cell(cellF).Value = dgvReport.Columns[6].Name;

                    /*Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center*/
                    worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellB).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellC).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellD).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellE).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellF).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;

                    /*default value for cell from a to f*/
                    cellA = &quot;A&quot;;
                    cellB = &quot;B&quot;;
                    cellC = &quot;C&quot;;
                    cellD = &quot;D&quot;;
                    cellE = &quot;E&quot;;
                    cellF = &quot;F&quot;;
                }
            }

            /*In this loop will perform the control of the variable index and prodceder&agrave; to the writing of the values ​​contained in 
             * the DataGrid on the variables from cell to celfl, so pore actually write on the cells of the sheet excel*/
            for (var riga = 0; riga &lt; dgvReport.Rows.Count; riga&#43;&#43;)
            {
                /*If index equals 3*/
                if (indexcell &gt; 3)
                {
                    /*Allowance for cells and and the numerical value given by the variable i and indexcell*/
                    cellA &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellB &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellC &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellD &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellE &#43;= indexcell.ToString(CultureInfo.InvariantCulture);
                    cellF &#43;= indexcell.ToString(CultureInfo.InvariantCulture);

                    /*Here instead we assign from cell to cell f the value of each row in the DataGrid control and always through their Value property*/
                    worksheet.Cell(cellA).Value = dgvReport.Rows[riga].Cells[1].Value;
                    worksheet.Cell(cellB).Value = dgvReport.Rows[riga].Cells[2].Value;
                    worksheet.Cell(cellC).Value = dgvReport.Rows[riga].Cells[3].Value;
                    worksheet.Cell(cellD).Value = dgvReport.Rows[riga].Cells[4].Value;
                    worksheet.Cell(cellE).Value = dgvReport.Rows[riga].Cells[5].Value;
                    worksheet.Cell(cellF).Value = dgvReport.Rows[riga].Cells[6].Value;

                    /*Check by enumeration XLAlignmentHorizontalValues​​, the alignment of text within the cell to be shown at the center*/
                    worksheet.Cell(cellA).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellB).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellC).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellD).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellE).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;
                    worksheet.Cell(cellF).Style.Alignment.Horizontal = XLAlignmentHorizontalValues.Center;

                    /*This method allows to adapt the text within the cells so that it is well centered and adapted to their inner*/
                    worksheet.Columns().AdjustToContents();

                    /*default value for cell from a to f*/
                    cellA = &quot;A&quot;;
                    cellB = &quot;B&quot;;
                    cellC = &quot;C&quot;;
                    cellD = &quot;D&quot;;
                    cellE = &quot;E&quot;;
                    cellF = &quot;F&quot;;
                }

                /*increase the value of the variable indexcell*/
                indexcell &#43;= 1;
            }

            /*Here we give the user the possibility scegiere where to save the file which will then be generated using the SaveFileDialog*/
            if (sfDialog.ShowDialog().Equals(DialogResult.OK))
            {
                /*This method will save the file in xlsx excel where the user decide this 
                 * by the argument required by that method where we spend the path of destination*/
                workbook.SaveAs(sfDialog.FileName);
            }
        }

        //BtnExitClick Event
        private void BtnExitClick(object sender, EventArgs e)
        {
            /*Close actual Form*/
            Close();
        }
    }
}</pre>
<div class="preview">
<pre class="vb"><span class="visualBasic__com">'dll&nbsp;netFramework</span>&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;System.Globalization&nbsp;
<span class="visualBasic__keyword">Imports</span>&nbsp;ClosedXML.Excel&nbsp;
&nbsp;
<span class="visualBasic__com">'FrmReport&nbsp;Class</span>&nbsp;
<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;FrmReport&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Sub&nbsp;FrmReport</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;FrmReport(<span class="visualBasic__keyword">ByVal</span>&nbsp;datareport&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;DataGridView)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Enhanced&nbsp;the&nbsp;value&nbsp;control&nbsp;DataGrid&nbsp;using&nbsp;the&nbsp;property&nbsp;DataReport</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dgvReport.DataSource&nbsp;=&nbsp;datareport.DataSource&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnExitClick&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnExitClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnExit.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Close&nbsp;actual&nbsp;Form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Close()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'BtnExportToExcelClick&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;BtnExportToExcelClick(sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;EventArgs)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;btnExportToExcel.Click&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;the&nbsp;DataGrid&nbsp;control&nbsp;does&nbsp;not&nbsp;contain&nbsp;any&nbsp;column</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;dgvReport.Columns.Count.Equals(<span class="visualBasic__number">0</span>)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;get&nbsp;a&nbsp;message&nbsp;to&nbsp;the&nbsp;user</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MessageBox.Show(My.Resources.FrmReport_BtnSalvaInExcelClick_Nessuna_riga_da_salvare,&nbsp;Application.ProductName.ToString(CultureInfo.InvariantCulture))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Return</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Imposed&nbsp;on&nbsp;the&nbsp;size&nbsp;of&nbsp;the&nbsp;file&nbsp;to&nbsp;be&nbsp;saved&nbsp;for&nbsp;the&nbsp;SaveFileDialog&nbsp;component,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'the&nbsp;format&nbsp;and&nbsp;saved&nbsp;in&nbsp;the&nbsp;application's&nbsp;resources.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sfDialog.Filter&nbsp;=&nbsp;My.Resources.FileXlsx&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Given&nbsp;the&nbsp;name&nbsp;of&nbsp;the&nbsp;excel&nbsp;file&nbsp;that&nbsp;will&nbsp;be&nbsp;generated.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sfDialog.FileName&nbsp;=&nbsp;<span class="visualBasic__string">&quot;USER&nbsp;DATA&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Here,&nbsp;however,&nbsp;we&nbsp;create&nbsp;a&nbsp;new&nbsp;worksheet&nbsp;excel</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;workbook&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;XLWorkbook()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'On&nbsp;the&nbsp;worksheet,&nbsp;create&nbsp;the&nbsp;worksheet&nbsp;in&nbsp;another&nbsp;sheet&nbsp;named&nbsp;user&nbsp;reports,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'this&nbsp;leaflet&nbsp;will&nbsp;be&nbsp;included&nbsp;in&nbsp;the&nbsp;excel&nbsp;file&nbsp;which&nbsp;will&nbsp;then&nbsp;be&nbsp;generated.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;worksheet&nbsp;=&nbsp;workbook.Worksheets.Add(<span class="visualBasic__string">&quot;USER&nbsp;DATA&nbsp;REPORT&quot;</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'I&nbsp;create&nbsp;variables&nbsp;as&nbsp;there&nbsp;are&nbsp;columns&nbsp;of&nbsp;excel&nbsp;file&nbsp;to&nbsp;be&nbsp;created,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'in&nbsp;this&nbsp;case&nbsp;6&nbsp;and&nbsp;the&nbsp;imposed&nbsp;with&nbsp;a&nbsp;default&nbsp;value</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellA&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellB&nbsp;=&nbsp;<span class="visualBasic__string">&quot;B&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellC&nbsp;=&nbsp;<span class="visualBasic__string">&quot;C&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellD&nbsp;=&nbsp;<span class="visualBasic__string">&quot;D&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellE&nbsp;=&nbsp;<span class="visualBasic__string">&quot;E&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;cellF&nbsp;=&nbsp;<span class="visualBasic__string">&quot;F&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;variable&nbsp;is&nbsp;used&nbsp;for&nbsp;the&nbsp;process&nbsp;of&nbsp;writing&nbsp;the&nbsp;various&nbsp;sections&nbsp;of&nbsp;the&nbsp;paper,&nbsp;the&nbsp;header,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'the&nbsp;name&nbsp;of&nbsp;the&nbsp;columns&nbsp;to&nbsp;end&nbsp;up&nbsp;with&nbsp;the&nbsp;values&nbsp;​​of&nbsp;the&nbsp;DataGrid&nbsp;control</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;indexcell&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'In&nbsp;this&nbsp;loop&nbsp;we&nbsp;perform&nbsp;the&nbsp;control&nbsp;of&nbsp;the&nbsp;variable&nbsp;index&nbsp;and&nbsp;it&nbsp;will&nbsp;create&nbsp;the&nbsp;header&nbsp;of&nbsp;the&nbsp;sheet,&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'a&nbsp;title&nbsp;and&nbsp;the&nbsp;formatting&nbsp;of&nbsp;cells&nbsp;on&nbsp;the&nbsp;alignment&nbsp;of&nbsp;the&nbsp;title&nbsp;text</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;riga&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;<span class="visualBasic__number">3</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'In&nbsp;this&nbsp;loop&nbsp;are&nbsp;enclosed&nbsp;in&nbsp;stages&nbsp;to&nbsp;the&nbsp;header&nbsp;in&nbsp;the&nbsp;title,&nbsp;the&nbsp;cell&nbsp;formatting&nbsp;and&nbsp;the&nbsp;column&nbsp;headings</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;indexcell&nbsp;&#43;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;index&nbsp;equals&nbsp;1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;indexcell.Equals(<span class="visualBasic__number">1</span>)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Allowance&nbsp;for&nbsp;cells&nbsp;and&nbsp;and&nbsp;the&nbsp;numerical&nbsp;value&nbsp;given&nbsp;by&nbsp;the&nbsp;variable&nbsp;i&nbsp;and&nbsp;indexcell</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'The&nbsp;Merge&nbsp;method&nbsp;allows&nbsp;to&nbsp;combine&nbsp;two&nbsp;or&nbsp;more&nbsp;cells,&nbsp;in&nbsp;this&nbsp;case&nbsp;we&nbsp;combine&nbsp;the&nbsp;cells&nbsp;from&nbsp;a&nbsp;to&nbsp;f</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Range(cellA&nbsp;&#43;&nbsp;<span class="visualBasic__string">&quot;:&quot;</span>&nbsp;&#43;&nbsp;cellF).Merge()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Assign&nbsp;a&nbsp;value&nbsp;to&nbsp;the&nbsp;cell,&nbsp;so&nbsp;that&nbsp;it&nbsp;can&nbsp;fill&nbsp;the&nbsp;contents&nbsp;of&nbsp;the&nbsp;cells&nbsp;to&nbsp;f</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Value&nbsp;=&nbsp;<span class="visualBasic__string">&quot;USER&nbsp;DATA&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Check&nbsp;by&nbsp;enumeration&nbsp;XLAlignmentHorizontalValues​​,&nbsp;the&nbsp;alignment&nbsp;of&nbsp;text&nbsp;within&nbsp;the&nbsp;cell&nbsp;to&nbsp;be&nbsp;shown&nbsp;at&nbsp;the&nbsp;center</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Style.Fill.BackgroundColor&nbsp;=&nbsp;XLColor.CornflowerBlue&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'default&nbsp;value&nbsp;for&nbsp;cell&nbsp;a&nbsp;and&nbsp;f</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;=&nbsp;<span class="visualBasic__string">&quot;F&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;index&nbsp;equals&nbsp;2</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;indexcell.Equals(<span class="visualBasic__number">2</span>)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Allowance&nbsp;for&nbsp;cells&nbsp;and&nbsp;and&nbsp;the&nbsp;numerical&nbsp;value&nbsp;given&nbsp;by&nbsp;the&nbsp;variable&nbsp;i&nbsp;and&nbsp;indexcell</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellB&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellC&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellD&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellE&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Here,&nbsp;however,&nbsp;we&nbsp;assign&nbsp;the&nbsp;cell&nbsp;to&nbsp;the&nbsp;cell&nbsp;f&nbsp;the&nbsp;name&nbsp;of&nbsp;the&nbsp;columns&nbsp;of&nbsp;the&nbsp;DataGrid&nbsp;control&nbsp;by&nbsp;property&nbsp;Value</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">1</span>).Name&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellB).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">2</span>).Name&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellC).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">3</span>).Name&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellD).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">4</span>).Name&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellE).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">5</span>).Name&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellF).Value&nbsp;=&nbsp;dgvReport.Columns(<span class="visualBasic__number">6</span>).Name&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Check&nbsp;by&nbsp;enumeration&nbsp;XLAlignmentHorizontalValues​​,&nbsp;the&nbsp;alignment&nbsp;of&nbsp;text&nbsp;within&nbsp;the&nbsp;cell&nbsp;to&nbsp;be&nbsp;shown&nbsp;at&nbsp;the&nbsp;center</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellB).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellC).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellD).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellE).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellF).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'default&nbsp;value&nbsp;for&nbsp;cell&nbsp;from&nbsp;a&nbsp;to&nbsp;f</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellB&nbsp;=&nbsp;<span class="visualBasic__string">&quot;B&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellC&nbsp;=&nbsp;<span class="visualBasic__string">&quot;C&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellD&nbsp;=&nbsp;<span class="visualBasic__string">&quot;D&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellE&nbsp;=&nbsp;<span class="visualBasic__string">&quot;E&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;=&nbsp;<span class="visualBasic__string">&quot;F&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'In&nbsp;this&nbsp;loop&nbsp;will&nbsp;perform&nbsp;the&nbsp;control&nbsp;of&nbsp;the&nbsp;variable&nbsp;index&nbsp;and&nbsp;prodceder&agrave;&nbsp;to&nbsp;the&nbsp;writing&nbsp;of&nbsp;the&nbsp;values&nbsp;​​contained&nbsp;in&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'the&nbsp;DataGrid&nbsp;on&nbsp;the&nbsp;variables&nbsp;from&nbsp;cell&nbsp;to&nbsp;celfl,&nbsp;so&nbsp;pore&nbsp;actually&nbsp;write&nbsp;on&nbsp;the&nbsp;cells&nbsp;of&nbsp;the&nbsp;sheet&nbsp;excel</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;riga&nbsp;=&nbsp;<span class="visualBasic__number">0</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;dgvReport.Rows.Count&nbsp;-&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'If&nbsp;index&nbsp;equals&nbsp;3</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;indexcell&nbsp;&gt;&nbsp;<span class="visualBasic__number">3</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Allowance&nbsp;for&nbsp;cells&nbsp;and&nbsp;and&nbsp;the&nbsp;numerical&nbsp;value&nbsp;given&nbsp;by&nbsp;the&nbsp;variable&nbsp;i&nbsp;and&nbsp;indexcell</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellB&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellC&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellD&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellE&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;&#43;=&nbsp;indexcell.ToString(CultureInfo.InvariantCulture)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Here&nbsp;instead&nbsp;we&nbsp;assign&nbsp;from&nbsp;cell&nbsp;to&nbsp;cell&nbsp;f&nbsp;the&nbsp;value&nbsp;of&nbsp;each&nbsp;row&nbsp;in&nbsp;the&nbsp;DataGrid&nbsp;control&nbsp;and&nbsp;always&nbsp;through&nbsp;their&nbsp;Value&nbsp;property</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">1</span>).Value&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellB).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">2</span>).Value&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellC).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">3</span>).Value&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellD).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">4</span>).Value&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellE).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">5</span>).Value&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellF).Value&nbsp;=&nbsp;dgvReport.Rows(riga).Cells(<span class="visualBasic__number">6</span>).Value&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Check&nbsp;by&nbsp;enumeration&nbsp;XLAlignmentHorizontalValues​​,&nbsp;the&nbsp;alignment&nbsp;of&nbsp;text&nbsp;within&nbsp;the&nbsp;cell&nbsp;to&nbsp;be&nbsp;shown&nbsp;at&nbsp;the&nbsp;center</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellA).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellB).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellC).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellD).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellE).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Cell(cellF).Style.Alignment.Horizontal&nbsp;=&nbsp;XLAlignmentHorizontalValues.Center&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;allows&nbsp;to&nbsp;adapt&nbsp;the&nbsp;text&nbsp;within&nbsp;the&nbsp;cells&nbsp;so&nbsp;that&nbsp;it&nbsp;is&nbsp;well&nbsp;centered&nbsp;and&nbsp;adapted&nbsp;to&nbsp;their&nbsp;inner</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;worksheet.Columns().AdjustToContents()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'default&nbsp;value&nbsp;for&nbsp;cell&nbsp;from&nbsp;a&nbsp;to&nbsp;f</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellA&nbsp;=&nbsp;<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellB&nbsp;=&nbsp;<span class="visualBasic__string">&quot;B&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellC&nbsp;=&nbsp;<span class="visualBasic__string">&quot;C&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellD&nbsp;=&nbsp;<span class="visualBasic__string">&quot;D&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellE&nbsp;=&nbsp;<span class="visualBasic__string">&quot;E&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cellF&nbsp;=&nbsp;<span class="visualBasic__string">&quot;F&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'increase&nbsp;the&nbsp;value&nbsp;of&nbsp;the&nbsp;variable&nbsp;indexcell</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;indexcell&nbsp;&#43;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'Here&nbsp;we&nbsp;give&nbsp;the&nbsp;user&nbsp;the&nbsp;possibility&nbsp;scegiere&nbsp;where&nbsp;to&nbsp;save&nbsp;the&nbsp;file&nbsp;which&nbsp;will&nbsp;then&nbsp;be&nbsp;generated&nbsp;using&nbsp;the&nbsp;SaveFileDialog</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;sfDialog.ShowDialog().Equals(DialogResult.OK)&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'This&nbsp;method&nbsp;will&nbsp;save&nbsp;the&nbsp;file&nbsp;in&nbsp;xlsx&nbsp;excel&nbsp;where&nbsp;the&nbsp;user&nbsp;decide&nbsp;this&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'by&nbsp;the&nbsp;argument&nbsp;required&nbsp;by&nbsp;that&nbsp;method&nbsp;where&nbsp;we&nbsp;spend&nbsp;the&nbsp;path&nbsp;of&nbsp;destination</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;workbook.SaveAs(sfDialog.FileName)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Class</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
Per un risultato finale del nostro file excel cos&igrave; strutturato.</div>
<div class="scriptcode"><img id="70772" src="70772-immagineclosedxml.png" alt="" width="1600" height="900"></div>
<p><em><em>&nbsp;</em></em></p>
<p>&nbsp;</p>
<h1>More Information</h1>
<p><em>&nbsp;</em></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div><em>
<div>Questo articolo&nbsp;e stato creato&nbsp;dalla collaborazione da parte di Piero Sbressa e Carmelo La Monica.Potete contattarli ai seguenti riferimenti.</div>
<div></div>
<div>Piero Sbressa</div>
<div></div>
<div><a href="mailto:pierosbressa@crystalweb.it">pierosbressa@crystalweb.it</a></div>
<div></div>
<div><a href="http://www.crystalweb.it/"><span style="text-decoration:underline"><span style="font-size:x-small"><span>www.crystalweb.it</span></span></span></a>
<br>
<span style="font-size:x-small">&nbsp;</span></div>
<div><span style="font-size:x-small">&nbsp;</span></div>
<div><span style="font-size:x-small">Carmelo La Monica</span></div>
<div><span style="font-size:x-small">&nbsp;</span></div>
<div><span style="font-size:x-small"><a href="http://community.visual-basic.it/carmelolamonica/default.aspx">http://community.visual-basic.it/carmelolamonica/default.aspx</a></span></div>
</em></div>