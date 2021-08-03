# printable_labels_pdf
Generate pdf file with printable labels


 ## CREATE A PDF FILE WITH LABELS EASELY:
You can get a pdf file with labels for print. It can set easely with any type of labels widths ang heights, papers, etc... You can draw a single border if you need it. You can get the pdf file generated into a browser, download, get a string of the pdf or save it to the server. 100% written in PHP (pure PHP). Mpdf library required.


 # REQUERIMENTS:
 
 - A minimum (minimum, minimum, minimum requeriments is needed). Tested on:
 		
    - Simple Raspberry pi (B +	512MB	700 MHz ARM11) with Raspbian Lite PHP7.3 (i love this gadgets)  :heart_eyes:
 		
    - VirtualBox Ubuntu Server 20.04.2 LTS (Focal Fossa) with PHP7.4.3

- **MPDF LIBRARY NEEDED TO BY INSTALLED: https://mpdf.github.io/**
- Ensure to add correct path at line 106:

          require_once __DIR__ . '/mpdf/vendor/autoload.php';
 
 
  # FILES:
 *printable_labels_pdf_class.php* -> **Main File**.
 
 *example.php* -> **Example File**.
 
 
 # INSTALLATION:
 A lot of easy :smiley:. It is written in PURE PHP. Only need to include the files. Tested on basic PHP installation
 
         require_once( 'csv_pair_file_class.php' );
         
* You need to install mpdf library. Remember to set writable mpdf/vendor/mpdf/mpdf/tmp. See https://mpdf.github.io/ documentation
** If you change the mpdf dir installation, make sure mpdf library is included in printable_labels_pdf_class.php at line 106 in printable_labels_pdf_class.php:

          require_once __DIR__ . '/mpdf/vendor/autoload.php';
 
 
# RESUME OF METHODS:

- **CREATE CSV PAIR OBJECT:**
 
*$printable_labels_pdf = new printable_labels_pdf( $labels_config );*

Example:

        $printable_labels_pdf = new printable_labels_pdf( $labels_config );



- **$labels_config CONFIGURATION VALUES:**

ALL MEASURES ARE IN CM.

- width_label: Width of each label (in cm.).
- height_label: Height of each label (in cm.).
- num_rows: Num of rows in the page.
- num_cols: Num of cols in the page. If not set, 2 cols by default.
- margin_left_page: Margin at left of page before begin first col of labels (in cm.). If not set, 0 by default.
- margin_top_page: Margin at top of page before begin first row of labels (in cm.). If not set, 0 by default.
- margin_right_label: margin between labels at right (in cm.). If not set, 0 by default.
- margin_bottom_label: margin between labels at bottom (in cm.). If not set, 0 by default.
- padding_left_label: space between border of label and html content inside the label, beginning at left (in cm.). If not set, 0 by default.
- padding_top_label: space between border of label and html content inside the label, beginning at top (in cm.). If not set, 0 by default.
- skip_first_row: set if you want to skip first row. Some printers cannot print the first row. You can to skip it (true|false). If not set, false by default.
- skip_last_row: set if you want to skip last row. Some printers cannot print the last row. You can to skip it (true|false). If not set, false by default.
- page_format: Measures of the page. You can to give a values or a string format. See https://mpdf.github.io/ documentation.
	// array: [210,297].
	// string format: 'A0’ - 'A10', 'B0' - 'B10', 'C0' - 'C10', '4A0', '2A0', 'RA0' - 'RA4', 'SRA0' - 'SRA4', 'Letter', 'Legal', 'Executive', 'Folio', 'Demy', 'Royal', 'A' (Type A paperback 111x178mm), 'B' (Type B paperback 128x198mm).
- page_orientation: Portrait or Landscape. ('P'|'L'). If not set, 'P'ortrait by default.
- default_font: String. If not set, 'Times'. See https://mpdf.github.io/ documentation for available fonts.
- default_font_size: In pixels. If not set, 0 that means CSS default.
- draw_border: (true|false). You can draw a border around the label. If not set, false that means without borders.
- start_at_label: For recicle paper, if you have printed some labels and remain labels in blank for print, you can use another time the paper, begin at label num. that you specify here. If not set, 1 that means at first label.
	
	
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
$printable_labels_pdf->get_labels_pdf('/some_dir/test.pdf', 'F'); // Save pdf in some dir of the server
  
  

 
 **Of course. You can use it freely :vulcan_salute::alien:**
 
 By Rafa.
 
 
 @author Rafael Martin Soto
 
 @author {@link http://www.inatica.com/ Inatica}
 
 @blog {@link https://rafamartin10.blogspot.com/ Rafael Martin's Blog}
 
 @since August 2021
 
 @version 1.0.0
 
 @license GNU General Public License v3.0
