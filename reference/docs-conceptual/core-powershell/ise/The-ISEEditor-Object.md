---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "ISEEditor 物件"
ms.assetid: 0101daf8-4e31-4e4c-ab89-01d95dcb8f46
ms.openlocfilehash: 41f2a6f7684275ad9d6d967ea67b64ca02c1c100
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2017
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="c7a1f-103">ISEEditor 物件</span><span class="sxs-lookup"><span data-stu-id="c7a1f-103">The ISEEditor Object</span></span>
  <span data-ttu-id="c7a1f-104">**ISEEditor** 物件是 Microsoft.PowerShell.Host.ISE.ISEEditor 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="c7a1f-105">主控台窗格是 **ISEEditor** 物件。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="c7a1f-106">每個 [ISEFile](The-ISEFile-Object.md) 物件都有相關聯的 **ISEEditor** 物件。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="c7a1f-107">下列各節將列出 **ISEEditor** 物件的方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="c7a1f-108">方法</span><span class="sxs-lookup"><span data-stu-id="c7a1f-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="c7a1f-109">Clear\(\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-109">Clear\(\)</span></span>
  <span data-ttu-id="c7a1f-110">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-111">清除編輯器中的文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-111">Clears the text in the editor.</span></span>

```PowerShell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="c7a1f-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-112">EnsureVisible\(int lineNumber\)</span></span>
  <span data-ttu-id="c7a1f-113">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-114">捲動編輯器，即會看見對應至指定 **lineNumber** 參數值的行。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="c7a1f-115">如果指定的行號不在 1 到最後一個定義有效行數的行號範圍內，即會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

 <span data-ttu-id="c7a1f-116">**lineNumber**
 要顯示的行號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-116">**lineNumber**
 The number of the line that is to be made visible.</span></span>

```PowerShell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="c7a1f-117">Focus\(\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-117">Focus\(\)</span></span>
  <span data-ttu-id="c7a1f-118">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-119">將焦點設定到編輯器。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-119">Sets the focus to the editor.</span></span>

```PowerShell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="c7a1f-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-120">GetLineLength\(int lineNumber \)</span></span>
  <span data-ttu-id="c7a1f-121">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-122">針對行號所指定的行，以整數形式設定行的長度。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

 <span data-ttu-id="c7a1f-123">**lineNumber**
 要取得長度的行號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-123">**lineNumber**
 The number of the line of which to get the length.</span></span>

 <span data-ttu-id="c7a1f-124">**Returns**
 位於指定行號之行的行長度。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-124">**Returns**
 The line length for the line at the specified line number.</span></span>

```PowerShell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="c7a1f-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-125">GoToMatch\(\)</span></span>
  <span data-ttu-id="c7a1f-126">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="c7a1f-127">如果編輯器物件的 **CanGoToMatch** 屬性是 **$true**，就會將插入號移到相符的字元，當插入號位於左括號、括號或大括號 (\(、\[、{) 正前方，或者在右括號、括號或大括號 (\)、\]、}) 正後方時即會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="c7a1f-128">插入號會放置於開端字元之前或結尾字元之後。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="c7a1f-129">如果 **CanGoToMatch** 屬性是 **$false**，則這個方法不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span> <span data-ttu-id="c7a1f-130">請參閱 [CanGoToMatch](#cangotomatch)。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-130">See [CanGoToMatch](#cangotomatch).</span></span>

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### <a name="inserttext-text-"></a><span data-ttu-id="c7a1f-131">InsertText\( text \)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-131">InsertText\( text \)</span></span>
  <span data-ttu-id="c7a1f-132">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-132">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-133">使用文字取代選取範圍，或在目前插入號位置插入文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-133">Replaces the selection with text or inserts text at the current caret position.</span></span>

 <span data-ttu-id="c7a1f-134">**text** - 字串：要插入的文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-134">**text** - String The text to insert.</span></span>

 <span data-ttu-id="c7a1f-135">請參閱本主題稍後的[指令碼範例](#example)。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-135">See the [Scripting Example](#example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="c7a1f-136">Select\( startLine, startColumn, endLine, endColumn \)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-136">Select\( startLine, startColumn, endLine, endColumn \)</span></span>
  <span data-ttu-id="c7a1f-137">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-137">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-138">從 **startLine**、**startColumn**、**endLine** 及 **endColumn** 參數選取文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-138">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

 <span data-ttu-id="c7a1f-139">**startLine** - 整數：選取範圍開始位置的行。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-139">**startLine** - Integer The line where the selection starts.</span></span>

 <span data-ttu-id="c7a1f-140">**startColumn** - 整數：選取範圍開始位置之起始行內的欄。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-140">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

 <span data-ttu-id="c7a1f-141">**endLine** - 整數：選取範圍結束位置的行。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-141">**endLine** - Integer The line where the selection ends.</span></span>

 <span data-ttu-id="c7a1f-142">**endColumn** - 整數：選取範圍結束位置之結尾行內的欄。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-142">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

 <span data-ttu-id="c7a1f-143">請參閱本主題稍後的[指令碼範例](#example)。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-143">See the  [Scripting Example](#example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="c7a1f-144">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-144">SelectCaretLine\(\)</span></span>
  <span data-ttu-id="c7a1f-145">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-145">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-146">選取目前包含插入號的整行文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-146">Selects the entire line of text that currently contains the caret.</span></span>

```PowerShell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="c7a1f-147">SetCaretPosition\( lineNumber, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-147">SetCaretPosition\( lineNumber, columnNumber \)</span></span>
  <span data-ttu-id="c7a1f-148">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-148">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-149">在行號和欄號設定插入號位置。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-149">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="c7a1f-150">如果插入號行號或插入號欄號不在其各自的有效範圍內，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-150">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

 <span data-ttu-id="c7a1f-151">**lineNumber** - 整數：插入號的行號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-151">**lineNumber** - Integer The caret line number.</span></span>

 <span data-ttu-id="c7a1f-152">**columnNumber** - 整數：插入號的欄號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-152">**columnNumber** - Integer The caret column number.</span></span>

```PowerShell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="c7a1f-153">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="c7a1f-153">ToggleOutliningExpansion\(\)</span></span>
  <span data-ttu-id="c7a1f-154">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="c7a1f-155">會展開或摺疊所有大綱區段。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-155">Causes all the outline sections to expand or collapse.</span></span>

```PowerShell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="c7a1f-156">[內容]</span><span class="sxs-lookup"><span data-stu-id="c7a1f-156">Properties</span></span>

###  <span data-ttu-id="c7a1f-157"><a name="CanGoToMatch"></a> CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="c7a1f-157"><a name="CanGoToMatch"></a> CanGoToMatch</span></span>
  <span data-ttu-id="c7a1f-158">在 Windows PowerShell ISE 3.0 與更新的版本中支援，而且不存在於之前的版本。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-158">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="c7a1f-159">唯讀的布林值屬性，可指出插入點是否位於括弧、括號或大括弧 (\(\)、\[\]、{}) 旁邊。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-159">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="c7a1f-160">如果插入號是在一組開端字元正前方或結尾字元的正後方，則這個屬性值會是 **$true**。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-160">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="c7a1f-161">否則為 **$false**。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-161">Otherwise, it is **$false**.</span></span>

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

###  <span data-ttu-id="c7a1f-162"><a name="CaretColumn"></a> CaretColumn</span><span class="sxs-lookup"><span data-stu-id="c7a1f-162"><a name="CaretColumn"></a> CaretColumn</span></span>
  <span data-ttu-id="c7a1f-163">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-163">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-164">唯讀屬性，可取得對應至插入號位置的欄號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-164">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```PowerShell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

###  <span data-ttu-id="c7a1f-165"><a name="CaretLine"></a> CaretLine</span><span class="sxs-lookup"><span data-stu-id="c7a1f-165"><a name="CaretLine"></a> CaretLine</span></span>
  <span data-ttu-id="c7a1f-166">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-166">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-167">唯讀屬性，可取得包含插入號的行號。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-167">The read-only property that gets the number of the line that contains the caret.</span></span>

```PowerShell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

###  <span data-ttu-id="c7a1f-168"><a name="CaretLineText"></a> CaretLineText</span><span class="sxs-lookup"><span data-stu-id="c7a1f-168"><a name="CaretLineText"></a> CaretLineText</span></span>
  <span data-ttu-id="c7a1f-169">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-169">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-170">唯讀屬性，可取得包含插入號的整行文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-170">The read-only property that gets the complete line of text that contains the caret.</span></span>

```PowerShell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

###  <span data-ttu-id="c7a1f-171"><a name="LineCount"></a> LineCount</span><span class="sxs-lookup"><span data-stu-id="c7a1f-171"><a name="LineCount"></a> LineCount</span></span>
  <span data-ttu-id="c7a1f-172">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-172">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-173">唯讀屬性，可從編輯器取得行數。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-173">The read-only property that gets the line count from the editor.</span></span>

```PowerShell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

###  <span data-ttu-id="c7a1f-174"><a name="SelectedText"></a> SelectedText</span><span class="sxs-lookup"><span data-stu-id="c7a1f-174"><a name="SelectedText"></a> SelectedText</span></span>
  <span data-ttu-id="c7a1f-175">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-175">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-176">唯讀屬性，可從編輯器取得選取的文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-176">The read-only property that gets the selected text from the editor.</span></span>

 <span data-ttu-id="c7a1f-177">請參閱本主題稍後的[指令碼範例](#example)。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-177">See the  [Scripting Example](#example) later in this topic.</span></span>

###  <span data-ttu-id="c7a1f-178"><a name="Text"></a> Text</span><span class="sxs-lookup"><span data-stu-id="c7a1f-178"><a name="Text"></a> Text</span></span>
  <span data-ttu-id="c7a1f-179">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-179">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c7a1f-180">唯讀屬性，可在編輯器中取得或設定文字。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-180">The read/write property that gets or sets the text in the editor.</span></span>

 <span data-ttu-id="c7a1f-181">請參閱本主題稍後的[指令碼範例](#example)。</span><span class="sxs-lookup"><span data-stu-id="c7a1f-181">See the [Scripting Example](#example) later in this topic.</span></span>

##  <span data-ttu-id="c7a1f-182"><a name="example"></a> 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="c7a1f-182"><a name="example"></a> Scripting Example</span></span>

```PowerShell
# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase. 
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor = $psISE.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line. 
$endColumn= $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1,1,3,$endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a><span data-ttu-id="c7a1f-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c7a1f-183">See Also</span></span>
- [<span data-ttu-id="c7a1f-184">ISEFile 物件</span><span class="sxs-lookup"><span data-stu-id="c7a1f-184">The ISEFile Object</span></span>](The-ISEFile-Object.md) 
- [<span data-ttu-id="c7a1f-185">PowerShellTab 物件</span><span class="sxs-lookup"><span data-stu-id="c7a1f-185">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="c7a1f-186">Windows PowerShell ISE 指令碼物件模型</span><span class="sxs-lookup"><span data-stu-id="c7a1f-186">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="c7a1f-187">Windows PowerShell ISE 物件模型參考</span><span class="sxs-lookup"><span data-stu-id="c7a1f-187">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="c7a1f-188">ISE 物件模型階層</span><span class="sxs-lookup"><span data-stu-id="c7a1f-188">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  