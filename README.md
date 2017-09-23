# Revd_Approver_Checker
Right now this program when ran in NX9 thru NX11 under Journaling (Created using Snap) creates a Dialog Box with 2 radio buttons with two catagories that talk to 3 list of options with 3 radio buttons REV'D BY, CHECKED BY, AND APPROVED BY. Within these 3 options are a list of persons responsible within the options. Sure there is large list of persons but when filtering by the radio buttons the dialog filters in the right person/persons. 

My next hurdle is after everything is set to process is to press OK  with the fields picked are for the drawing to populate. Lets, say Approved BY. What I know is APPROVED BY has an attribute "APPROVED_BY" and needs to be embedded into the NX properties dialog under part attributes along putting the required person when picked from the dialog on the drawing. The drawing size is "D" size and I do have locations from the X and Y cordinates in the drawing space. The X and Y cordinates are as follows. 27.13 in the "X" and .585 in the "Y".  Now with the name picked would not only populate the NX properties part attributes but would fall in that space using them dimensions for the APPROVED BY.
I have changed the names to protect the innocent.
Changed to colors for persons
Below is the code not finished
I used Snap in NX fOR THE CODE BELOW.




Option Infer OnImports Snap, Snap.Create
Public Class BoatForm : Inherits UI.BlockForm
   ' Declarations of the blocks on a BoatForm dialog       Dim menuBlock    As UI.Block.Enumeration    Dim menuBlock2   As UI.Block.Enumeration    Dim listBox    As UI.Block.ListBox      'Dim integerBlock As UI.Block.Integer
    Dim SmallBoatsRevBy As String() = {"Red", "White", "Blue", "Cyan"}
    Dim SmallBoatsCheckedBy As String() = {"Blue", "Cyan"}
    Dim SmallBoatsApprovedBy As String() = {"Black"}
    Dim LargeBoatsRevBy As String() = {"Orange","Plum","Apple","Pear"}
    Dim LargeBoatsCheckedBy As String() = {"Orange","Plum","Apple"}
    Dim LargeBoatsApprovedBy As String() = {"Orange"}
    Dim people As String(,)() = {{SmallBoatsRevBy, SmallBoatsCheckedBy, SmallBoatsApprovedBy}, {LargeBoatsRevBy, LargeBoatsCheckedBy, LargeBoatsApprovedBy}}
    Public Sub New()
        Me.Title = "Boat Form"  'Title of the Dialog        Me.Cue = "Please enter information"           'Must Have to enter information
        ' Create an option menu block        menuBlock = New UI.Block.Enumeration()        menuBlock.Label = "Please choose option"        menuBlock.Items = {"Small Boats", "Large Boats"}        menuBlock.PresentationStyle = UI.Block.EnumPresentationStyle.RadioBox        menuBlock.Layout = UI.Block.Layout.Horizontal   ' Creates an Integer block1
        ' Create an option menu block2        menuBlock2 = New UI.Block.Enumeration()        menuBlock2.Label = "Please choose option"        menuBlock2.Items = {"Rev'd By", "Checked By", "Approved By"}        menuBlock2.PresentationStyle = UI.Block.EnumPresentationStyle.RadioBox        menuBlock2.Layout = UI.Block.Layout.Horizontal      ' Creates an Integer block2
        'Create list box to hold Rev'd By, Checked By, Approved By names
        listBox = New UI.Block.ListBox()        listBox.SingleSelect = True        listBox.ListItems = people(0, 0)        listBox.Height = 8
        listBox.BeginGroup = True        listBox.Label = menuBlock.Items(menuBlock.Value) & ": " & menuBlock2.Items(menuBlock2.Value)
        ' Adds the Three blocks to the BlockForm and a List Box        Me.AddBlocks(menuBlock, menuBlock2, listBox)
    End Sub
   Public Shared Sub Main() 'This is where the program starts and jumps around
      Dim myForm = New BoatForm()      myForm.Show()
   End Sub
    Public Overrides Sub OnUpdate(changedBlock As Snap.UI.Block.General)        If changedBlock = menuBlock Or changedBlock = menuBlock2 Then            listBox.ListItems = people(menuBlock.Value, menuBlock2.Value)            listBox.Label = menuBlock.Items(menuBlock.Value) & ": " & menuBlock2.Items(menuBlock2.Value)        End If    End Sub
   Public Overrides Sub OnApply()
' This is where the action of what is picked will happen.
   End Sub
End Class
