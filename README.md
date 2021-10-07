# printable_labels_pdf
Generate pdf file with printable labels with PHP code.


 ## CREATE A PDF FILE WITH LABELS EASELY:
You can get a pdf file with labels for print. It can set easely with any type of labels widths ang heights, papers, etc... You can draw a single border if you need it. You can get the pdf file generated into a browser, download, get a string of the pdf or save it to the server. 100% written in PHP (pure PHP). Mpdf library required.

# SCREENSHOTS:
![Screenshot of the pdf labels created in Pure PHP](https://github.com/vivesweb/printable_labels_pdf/blob/main/test_pdf_labels.png?raw=true)

Test with VirtualBox Ubuntu Server 20.04.2 LTS (Focal Fossa) with PHP7.4.3 in 18 seconds.


![Screenshot of the pdf labels created in Pure PHP](https://github.com/vivesweb/printable_labels_pdf/blob/main/test_pdf_labels_2.png?raw=true)

Content of the pdf created.

# You can see a test result here:

https://github.com/vivesweb/printable_labels_pdf/blob/main/pritable_labels_pdf.pdf


 # REQUERIMENTS:
 
 - A minimum (minimum, minimum, minimum requeriments is needed). Tested on:
 		
    - Simple Raspberry pi (B +	512MB	700 MHz ARM11) with Raspbian Lite PHP7.3 (i love this gadgets)  :heart_eyes:
 		
    - VirtualBox Ubuntu Server 20.04.2 LTS (Focal Fossa) with PHP7.4.3

    - Red Hat Enterprise Linux Server release 6.10 (Santiago) PHP Version 7.3.25 (Production Server) 512Mb Memory Limit

    - Red Hat Enterprise Linux release 8.4 (Ootpa). PHP Version 8.0.11 (Production Server) 512Mb Memory Limit

- **MPDF LIBRARY NEEDED TO BY INSTALLED: https://mpdf.github.io/**
- Ensure to add correct path at line 106 in the file _printable_labels_pdf_class.php_:

          require_once __DIR__ . '/mpdf/vendor/autoload.php';
 
 
# FILES:
 *printable_labels_pdf_class.php* -> **Main File**.
 
 *example.php* -> **Example File**.
 
 *pritable_labels_pdf.pdf* -> **Example pdf with labels File created**.
 
 *test_pdf_labels.png* -> **Screenshot of a pdf file created**.
 
 *test_pdf_labels_2.png* -> **Screenshot of the content data inside the pdf (with benchmark)**.
 
 
 # INSTALLATION:
 A lot of easy :smiley:. It is written in PURE PHP. Only need to include the files. Tested on basic PHP installation
 
         require_once( 'printable_labels_pdf_class.php' );
         
* You need to install mpdf library. Remember to set writable mpdf/vendor/mpdf/mpdf/tmp. See https://mpdf.github.io/ documentation
* If you change the mpdf dir installation, make sure mpdf library is included in printable_labels_pdf_class.php at line 106 in printable_labels_pdf_class.php:

          require_once __DIR__ . '/mpdf/vendor/autoload.php';
 
 
# RESUME OF METHODS:

- **CREATE PRINTABLE LABELS PDF OBJECT:**
 
*$printable_labels_pdf = new printable_labels_pdf( $labels_config );*

Example:

        $printable_labels_pdf = new printable_labels_pdf( $labels_config );



- **$labels_config CONFIGURATION VALUES:**

ALL MEASURES ARE IN CM.

- _width_label_: Width of each label (in cm.).
- _height_label_: Height of each label (in cm.).
- _num_rows_: Num of rows in the page.
- _num_cols_: Num of cols in the page. If not set, 2 cols by default.
- _margin_left_page_: Margin at left of page before begin first col of labels (in cm.). If not set, 0 by default.
- _margin_top_page_: Margin at top of page before begin first row of labels (in cm.). If not set, 0 by default.
- _margin_left_label_: margin between labels at left (in cm.). If not set, 0 by default.
- _margin_bottom_label_: margin between labels at bottom (in cm.). If not set, 0 by default.
- _padding_left_label_: space between border of label and html content inside the label, beginning at left (in cm.). If not set, 0 by default.
- _padding_top_label_: space between border of label and html content inside the label, beginning at top (in cm.). If not set, 0 by default.
- _skip_first_row_: set if you want to skip first row. Some printers cannot print the first row. You can to skip it (true|false). If not set, false by default.
- _skip_last_row_: set if you want to skip last row. Some printers cannot print the last row. You can to skip it (true|false). If not set, false by default.
- _page_format_: Measures of the page ('A4', for example). You can to give a values or a string format. See https://mpdf.github.io/ documentation.

	// array: [210,297].
	
	// string format: 'A0’ - 'A10', 'B0' - 'B10', 'C0' - 'C10', '4A0', '2A0', 'RA0' - 'RA4', 'SRA0' - 'SRA4', 'Letter', 'Legal', 'Executive', 'Folio', 'Demy', 'Royal', 'A' (Type A paperback 111x178mm), 'B' (Type B paperback 128x198mm).
	
- _page_orientation_: Portrait or Landscape. ('P'|'L'). If not set, 'P'ortrait by default.
- _default_font_: String. If not set, 'Times'. See https://mpdf.github.io/ documentation for available fonts.
- _default_font_size_: In pixels. If not set, 0 that means CSS default.
- _draw_border_: (true|false). You can draw a border around the label. If not set, false that means without borders.
- _start_at_label_: To recycle paper, if you have printed some labels and remain labels in blank for print, you can use another time the paper, begin at label num. that you specify here. If not set, 1 that means at first label. :recycle: :smiley:
	
	
 The distribution of number labels:
	
	---------------------
	| label 1 | label 2 |
	---------------------
	| label 3 | label 4 |
	---------------------
	| label 5 | label 6 |
	---------------------
	| label 7 | label 8 |
	---------------------
	| label 9 | label 10|
	---------------------
	
		
	Ex. Maybe you have a page printed labels from 1 to 5, and then have the rest labels in blank, without print.
	You can recycle the labels paper and use it another time!!!!
	If you want to print the first label beginning at position 6 (that is 3 row second col), then set $begin_at_label_num to 6
	For our example, the pdf will be created as it:
	---------------------
	| skipped | skipped |
	---------------------
	| skipped | skipped |
	---------------------
	| skipped | label 6 |
	---------------------
	| label 7 | label 8 |
	---------------------
	| label 9 | label 10|
	---------------------
	
	
	IMPORTANT!!!! if you skip first row, the id's keep its natural order:
	
	---------------------
	| skipped | skipped |
	---------------------
	| label 3 | label 4 |
	---------------------
	| label 5 | label 6 |
	---------------------
	| label 7 | label 8 |
	---------------------
	| label 9 | label 10|
	---------------------
	
	Then, if whe skip first row and set $begin_at_label_num with 1, 2 or 3,
	will have the same result because in all the cases it will begin at label 3
	
	
	
- **DRAW BORDERS:**

*$printable_labels_pdf->draw_border( true );*

*Draw a border around the labels*


Example:

        $printable_labels_pdf->draw_border( true );



- **WRITE LABEL:**

*$printable_labels_pdf->write_label( $label_html );*
*Send a content html for draw new label*

- You can use standard html tags as < b > bold, < i > italic, < u > underline or other. See example.php with some lines in different formats.

Example:

        // Make a string of the html label
	      $label_html  = '<b>label bold</b><br />';       // 1st row. Bold
	      $label_html .= '<i>Line 2 italic</i><br />';    // 2nd row. Italic
	      $label_html .= '<u>Line 3 underline</u><br />'; // 3th row. Underline
	      $label_html .= 'Line 4 normal';                 // 4th row. Standard text
	
	      // send the html string to a new label
	      $printable_labels_pdf->write_label( $label_html );



- **GET PDF WITH LABELS:**

*$printable_labels_pdf->get_labels_pdf( $file_name, $output);*
*return the pdf in the browser in the output format*

Examples:

        $printable_labels_pdf->get_labels_pdf( $file_name, $output);
	
**a) Show directly in the browser (default)**

$printable_labels_pdf->get_labels_pdf('test.pdf', 'I'); // Output a PDF file directly to the browser



**b) Get a String of the pdf to do something with it later:**

$SomeVarPdfString = $printable_labels_pdf->get_labels_pdf('test.pdf', 'S'); // Get pdf in string format and assign to $SomeVarPdfString



**c) Download**

$printable_labels_pdf->get_labels_pdf('test.pdf', 'D'); // Download pdf



**d) Save pdf file in server path**

$printable_labels_pdf->get_labels_pdf('/some_dir/test.pdf', 'F'); // Save pdf in some dir of the server. Ensure that you have writable perms to the folder
  
  
  
**BENCHMARK:**
 
You have included a Benchmark in the internal data of pdf properties (see creator application data) :smiley:
 
 Configuration TEST in Virtual Ubuntu Linux:
 - Num labels: 2.499
 - 4 lines each label
 - Line 1: Bold
 - Line 2: italic
 - Line 3: underline
 - Line 4: normal
 - Format Page: A4
 - Distribution of labels 2 cols x 12 rows
 - Skip first row: true
 - Skip last row: true
 - Print Border: true
 - Begin at label 4
 - Label Width: 8.89
 - Label height: 2.33
 - margin_left_page: 1.3
 - margin_top_page: .2
 - margin_left_label: .2
 - margin_bottom_label: .2
 - padding_left_label: .25
 - padding_top_label: .25
  
 RESULT:
 - 125 pages created in 18 seconds
 
* See the original pdf created for benchmark here: https://github.com/vivesweb/printable_labels_pdf/blob/main/pritable_labels_pdf.pdf

In a simple Raspberry PI b 2 i get with the same config, with 999 labels, done in 2 minutes and 28 seconds :sweat_smile:

**SOME NOTES:**

I find some bugs floating divs and margins in mpdf. Only works with margin-left and margin-bottom label, but don't worry, there is no problem. All works ok :smile:.
 
 **Of course. You can use it freely :vulcan_salute::alien:**
 
 By Rafa.
 
 
 @author Rafael Martin Soto
 
 @author {@link http://www.inatica.com/ Inatica}
 
 @blog {@link https://rafamartin10.blogspot.com/ Rafael Martin's Blog}
 
 @since August 2021
 
 @version 1.0.0
 
 @license GNU General Public License v3.0
