---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "建立自訂輸入方塊"
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 52f2556267af1e53ee823868f64138e67673beba
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="9285a-103">建立自訂輸入方塊</span><span class="sxs-lookup"><span data-stu-id="9285a-103">Creating a Custom Input Box</span></span>
<span data-ttu-id="9285a-104">使用 Windows PowerShell 3.0 和更新版本中 Microsoft .NET Framework 的表單建立功能，撰寫圖形化自訂輸入方塊的指令碼。</span><span class="sxs-lookup"><span data-stu-id="9285a-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="9285a-105">建立自訂的圖形化輸入方塊</span><span class="sxs-lookup"><span data-stu-id="9285a-105">Create a custom, graphical input box</span></span>
<span data-ttu-id="9285a-106">將下列程式碼複製並貼上到 Windows PowerShell ISE，然後將它儲存為 Windows PowerShell 指令碼 (.ps1)。</span><span class="sxs-lookup"><span data-stu-id="9285a-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please enter the information in the space below:"
$form.Controls.Add($label) 

$textBox = New-Object System.Windows.Forms.TextBox 
$textBox.Location = New-Object System.Drawing.Point(10,40) 
$textBox.Size = New-Object System.Drawing.Size(260,20) 
$form.Controls.Add($textBox) 

$form.Topmost = $True

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

<span data-ttu-id="9285a-107">指令碼一開始會載入兩個 .NET Framework 類別：**System.Drawing** 和 **System.Windows.Forms**。</span><span class="sxs-lookup"><span data-stu-id="9285a-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="9285a-108">接著，您會啟動新的 .NET Framework 類別 **System.Windows.Forms.Form** 的執行個體，這樣可以提供空白表單或視窗讓您可以開始新增控制項。</span><span class="sxs-lookup"><span data-stu-id="9285a-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="9285a-109">建立 Form 類別的執行個體之後，指派值給此類別的三個屬性。</span><span class="sxs-lookup"><span data-stu-id="9285a-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

-   <span data-ttu-id="9285a-110">**Text**。</span><span class="sxs-lookup"><span data-stu-id="9285a-110">**Text.**</span></span> <span data-ttu-id="9285a-111">這會成為視窗的標題。</span><span class="sxs-lookup"><span data-stu-id="9285a-111">This becomes the title of the window.</span></span>

-   <span data-ttu-id="9285a-112">**Size**。</span><span class="sxs-lookup"><span data-stu-id="9285a-112">**Size.**</span></span> <span data-ttu-id="9285a-113">這是表單的大小，單位為像素。</span><span class="sxs-lookup"><span data-stu-id="9285a-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="9285a-114">上述指令碼會建立 300 像素寬、200 像素高的表單。</span><span class="sxs-lookup"><span data-stu-id="9285a-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

-   <span data-ttu-id="9285a-115">**StartingPosition**。</span><span class="sxs-lookup"><span data-stu-id="9285a-115">**StartingPosition.**</span></span> <span data-ttu-id="9285a-116">此選擇性屬性在上述指令碼中是設定為 **CenterScreen**。</span><span class="sxs-lookup"><span data-stu-id="9285a-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="9285a-117">若未新增此屬性，Windows 會在表單開啟時選取一個位置。</span><span class="sxs-lookup"><span data-stu-id="9285a-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="9285a-118">透過將 **StartingPosition** 設定為 **CenterScreen**，您可以在每次載入表單時，將表單自動顯示在畫面中間。</span><span class="sxs-lookup"><span data-stu-id="9285a-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"
```

<span data-ttu-id="9285a-119">接著，為您的表單建立 **[確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9285a-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="9285a-120">指定 **[確定]** 按鈕的大小與行為。</span><span class="sxs-lookup"><span data-stu-id="9285a-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="9285a-121">在此範例中，按鈕位置是距離表單上邊緣 120 像素，並距離左邊緣 75 像素。</span><span class="sxs-lookup"><span data-stu-id="9285a-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="9285a-122">按鈕高度是 23 像素，而按鈕寬度是 75 像素。</span><span class="sxs-lookup"><span data-stu-id="9285a-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="9285a-123">指令碼會使用預先定義的 Windows Forms 類型來決定按鈕行為。</span><span class="sxs-lookup"><span data-stu-id="9285a-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="9285a-124">同樣地，您也會建立 **[取消]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9285a-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="9285a-125">**[取消]** 按鈕距離上邊緣 120 像素，但距離視窗左邊緣 150 像素。</span><span class="sxs-lookup"><span data-stu-id="9285a-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="9285a-126">接下來，在您的視窗上提供標籤文字，以描述您希望使用者提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="9285a-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please enter the information in the space below:"
$form.Controls.Add($label)
```

<span data-ttu-id="9285a-127">新增控制項 (在此範例中為文字方塊)，讓使用者提供您在標籤文字中描述的資訊。</span><span class="sxs-lookup"><span data-stu-id="9285a-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="9285a-128">除了文字方塊外，還有許多其他您可以套用的控制項；如需更多控制項，請參閱 MSDN 上的 [System.Windows.Forms Namespace (System.Windows.Forms 命名空間)](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9285a-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```
$textBox = New-Object System.Windows.Forms.TextBox 
$textBox.Location = New-Object System.Drawing.Point(10,40) 
$textBox.Size = New-Object System.Drawing.Size(260,20) 
$form.Controls.Add($textBox)
```

<span data-ttu-id="9285a-129">將 **Topmost** 屬性設定為 **$True**，以強制視窗開啟在其他已開啟視窗與對話方塊的上方。</span><span class="sxs-lookup"><span data-stu-id="9285a-129">Set the **Topmost** property to **$True** to force the window to open atop other open windows and dialog boxes.</span></span>

```
$form.Topmost = $True
```

<span data-ttu-id="9285a-130">接下來，新增這行程式碼來啟動表單，並將焦點設定在您建立的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9285a-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="9285a-131">新增下面這行程式碼，以在 Windows 中顯示該表單。</span><span class="sxs-lookup"><span data-stu-id="9285a-131">Add the following line of code to display the form in Windows.</span></span>

```
$result = $form.ShowDialog()
```

<span data-ttu-id="9285a-132">最後，**If** 區塊內的程式碼會指示 Windows 當使用者在文字方塊中提供文字並按一下 **[確定]** 按鈕或按下 **Enter** 鍵時要執行的表單動作。</span><span class="sxs-lookup"><span data-stu-id="9285a-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="9285a-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9285a-133">See Also</span></span>
- [<span data-ttu-id="9285a-134">Hey Scripting Guy：Why don’t these PowerShell GUI examples work?</span><span class="sxs-lookup"><span data-stu-id="9285a-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644) (Hey Scripting Guy：PowerShell GUI 範例為什麼動不起來？)
- [<span data-ttu-id="9285a-135">GitHub：Dave Wyatt's WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="9285a-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates) (GitHub：Dave Wyatt 的 WinFormsExampleUpdates)
- [<span data-ttu-id="9285a-136">Windows PowerShell Tip of the Week: Creating a Custom Input Box</span><span class="sxs-lookup"><span data-stu-id="9285a-136">Windows PowerShell Tip of the Week:  Creating a Custom Input Box</span></span>](http://technet.microsoft.com/library/ff730941.aspx) (本週 Windows PowerShell 秘訣︰建立自訂輸入方塊)
