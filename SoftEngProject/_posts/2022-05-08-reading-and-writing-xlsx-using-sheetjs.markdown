---
layout: post
title:  "Reading and Writing Xlxs using Sheetjs"
author: hori75
date:   2022-05-08 18:50:00 +0700
background: '/images/sheetjs.png'
excerpt_separator: <!--more-->
---

Reading an excel file directly is not as easy as reading csv.
<!--more-->
XLSX file is a zipped XML-based file that represent a spreadsheet file as part of Microsoft Office Open XML specification.
Spreadsheet file from Microsoft Excel was saved in form of XLS before being replace with this file format.
The data is saved in compressed form so it couldn't be read directly by simple parsing script.

There are many parsing libraries for this file as it's used widely and there is a need to convert the data to save in other form.
In javascript, we can use SheetJS to parse and create XLSX file.
SheetJS has the community version with adequate features, its Pro version has more features beyond the basic of reading and writing XLSX file.
Here's a guide on how to use it on React. 

### Adding Xlsx module into react project

To add module into react project, we just add them into `package.json` using the following command.

```
npm install xlsx
pnpm install xlsx
yarn add xlsx
```

To use the module, we declare import on the script like this

```
import * as XLSX from "xlsx";
```

### Reading Xlsx

The example use case is reading Xlsx file after being selected from file input.
Here's the example function that handles the reading (in typescript). 

```
  const fileInputHandler = (event: React.ChangeEvent<HTMLInputElement>) => {
    if (event.target.files == null) return;
    const file = event.target.files[0];
    const reader = new FileReader();

    reader.onload = (event: ProgressEvent<FileReader>) => {
      if (event.target == null) return;
      const bstr = event.target.result;
      const wb = XLSX.read(bstr, { type: "binary" });
      const wsname = wb.SheetNames[0];
      const ws = wb.Sheets[wsname];
      const data: string[][] = XLSX.utils.sheet_to_json(ws, { header: 1 });
      console.log(data);
    };
    reader.readAsBinaryString(file);
  }
```

This creates a new file reader that uses `XLSX.read` to read binary data it gets from file reader.
After reading, it becomes a workbook object. A workbook stores one or many worksheets, we are getting the first worksheet.
From there, we convert it into an array of arrays to be printed on console log.
You could turn worksheet data into html table, csv, or json data in example above.

### Writing Xlsx

To generate new workbook, we use the following code.

```
var workbook = XLSX.utils.book_new();
```

This generates an empty workbook with no worksheets. 
Spreadsheet is enforced to have at least one worksheet, this is enforced on library if you would write the workbook
(it throws error if you try to generate Xlsx from empty workbook).

Previously we convert from worksheet into html, csv, or json.
We could convert the other way using `XLSX.utils.*_to_sheet(data, opt)` (just switch the other way).

To append a worksheet into workbook we use this code.

```
XLSX.utils.book_append_sheet(workbook, worksheet, sheet_name);
```

Take note that `sheet_name` should be unique between the worksheets in the workbook.
You could replace the worksheet by assigning a worksheet like this.

```
workbook.Sheets[sheet_name] = new_worksheet;
```

To write into Xlsx, we use `writeFile(wb, filename)`

```
XLSX.writeFile(wb, filename, write_opts)
```

### Conclusion

Sheetjs is a library created to write and read xlsx files. It has many variety of commands to use
and attempts to accomodate any common use cases.

### References

[Sheetjs community version](https://github.com/sheetjs/sheetjs)
