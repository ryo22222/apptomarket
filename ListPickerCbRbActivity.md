# Introduction #
An example to show how to create list pickers that have either Checkboxes or RadioButtons.

**NOTE:** This is currently included in the NightlyBuild and will later be in the next official release


# Details #

Now, you can create a list that includes Checkboxes OR Radiobuttons. Setup and initialization is pretty much like usual ListPicker. See download section (ListPickerCbRbActivity.java ) for full code example. Here is how output looks like:
<br><img src='http://www.3nportal.com/wikiImages/listPicker.jpg' />

<pre><code><br>
import com.google.devtools.simple.runtime.components.Component;<br>
import com.google.devtools.simple.runtime.components.HandlesEventDispatching;<br>
import com.google.devtools.simple.runtime.components.android.*;<br>
import com.google.devtools.simple.runtime.components.android.util.CsvUtil;<br>
import com.google.devtools.simple.runtime.components.util.YailList;<br>
import com.google.devtools.simple.runtime.events.EventDispatcher;<br>
<br>
import java.util.Arrays;<br>
<br>
<br>
public class ListPickerCbRbActivity extends Form implements HandlesEventDispatching {<br>
<br>
//Declare 2 ListPickerCheckbox, one for checkbox, the other for radio button examples<br>
ListPickerCheckbox listPickerCheckboxMulti;<br>
ListPickerCheckbox listPickerCheckboxRb;<br>
<br>
//declare 2 buttons. We display these buttons and once clicked, open their associated picker<br>
Button btnCb;<br>
Button btnRb;<br>
<br>
TextBox txtCsvItems;   //we use this to enter CSV data and load our picker with data of this text<br>
TextBox txtResults;    //A textbox used for debug purpose<br>
<br>
//create the layout<br>
void $define() {<br>
//init visual components<br>
btnCb = new Button(this, "Click for picker in checkboxes style", LENGTH_FILL_PARENT);<br>
btnRb = new Button(this, "Click for picker in radio button style", LENGTH_FILL_PARENT);<br>
<br>
new Label(this, "Enter listbox data in csv format:");<br>
<br>
//load some default data<br>
txtCsvItems = new TextBox(this, "item1, item2, item3", LENGTH_FILL_PARENT);<br>
<br>
listPickerCheckboxMulti = new ListPickerCheckbox(this);<br>
listPickerCheckboxRb = new ListPickerCheckbox(this);<br>
<br>
listPickerCheckboxMulti.Visible(false);<br>
listPickerCheckboxRb.Visible(false);<br>
<br>
//Use SelectionStlye to specify if we want multi (checkbox) or single (radio button)<br>
listPickerCheckboxMulti.SelectionStlye(Component.MULTIPLE_CHOICE);<br>
listPickerCheckboxRb.SelectionStlye(Component.SINGLE_CHOICE);<br>
<br>
//for debug purpose, we display results from our listpicker in this text box<br>
txtResults = new TextBox(this, "Results display here", Component.LENGTH_FILL_PARENT);<br>
<br>
//register for these events<br>
EventDispatcher.registerEventForDelegation(this, "test", "Click");<br>
EventDispatcher.registerEventForDelegation(this, "test", "AfterPicking");<br>
}<br>
<br>
@Override<br>
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args) {<br>
<br>
if (eventName.equals("Click")) {<br>
//A visual component was clicked<br>
if (component.equals(btnCb)) {<br>
refreshData();<br>
//we want to open listpicker in checkbox style<br>
listPickerCheckboxMulti.Open();<br>
return true;<br>
}<br>
else if (component.equals(btnRb)) {<br>
refreshData();<br>
//we want to open listpicker in radiobutton style<br>
listPickerCheckboxRb.Open();<br>
return true;<br>
}<br>
<br>
return false;<br>
<br>
}<br>
else if (eventName.equals("AfterPicking") &amp;&amp; component.equals(listPickerCheckboxMulti)) {<br>
//Get list of selection results. The Selections() will return boolean array of true or false for the list<br>
boolean[] selections = listPickerCheckboxMulti.Selections();<br>
<br>
//code below shows how to check and see if 3rd item is checked or not; 1st element is at position 0<br>
if (selections[2]) {<br>
//TODO: 2nd item was checked, add proper logic here<br>
}<br>
<br>
//convert boolean array into string for displaying result into our textbox field<br>
txtResults.Text(Arrays.toString(selections));<br>
return true;<br>
}<br>
else if (eventName.equals("AfterPicking") &amp;&amp; component.equals(listPickerCheckboxRb)) {<br>
//Get list of selection results. The Selections() will return boolean array of true or false for the list<br>
boolean[] selections = listPickerCheckboxRb.Selections();<br>
<br>
//code below shows how to check and see if 3rd item is checked or not; 1st element is at position 0<br>
if (selections[2]) {<br>
//TODO: 2nd item was checked, add proper logic here<br>
}<br>
<br>
//convert boolean array into string for displaying result into our textbox field<br>
txtResults.Text(Arrays.toString(selections));<br>
return true;<br>
}<br>
<br>
return false;<br>
}<br>
<br>
/**<br>
* Helper method to load our pickers with data that is in the text box<br>
*/<br>
private void refreshData() {<br>
YailList yailList = null;<br>
try {<br>
yailList = CsvUtil.fromCsvRow(txtCsvItems.Text());<br>
} catch (Exception e) {<br>
System.out.println("Error in parser: " + e.getMessage());<br>
//TODO: handle error<br>
}<br>
<br>
//Set the above items into our sample listpickers.<br>
// We are setting same items into both of our listpickers<br>
listPickerCheckboxRb.Elements(yailList);<br>
listPickerCheckboxMulti.Elements(yailList);<br>
<br>
}<br>
<br>
}<br>
</code></pre>

<b>NOTE:</b> You must include the following permission in your androidmanifest:<br>
<br>
<activity android:name="com.google.devtools.simple.runtime.components.android.ListPickerCheckboxActivity" />