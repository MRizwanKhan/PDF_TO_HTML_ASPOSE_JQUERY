## Web API PDF to HTML Converter using Aspose.Pdf & JQuery

### Introduction
This solution allow users to upload PDF file to server using Web API call as JQuery and converts the PDF to HTML file using Aspose.Pdf feature and returns generated HTML from PDF to client. This initial version of the application is enriched with the following cool features to make the PDF to HTML converting process simple and easy to use.

### Features in this Release
The release of this application supports the following features.
* REST enabled [Web API](http://www.asp.net/web-api).
* Allow user to upload PDF file to server.
* Verify the uploaded file for valid PDF.
* Display progressbar while processing.
* Converts PDF to HTML/HTML5 using Aspose.Pdf.
* Returns HTML string to client
* Display generated HTML in client web browser.
* Jquery file upload, progressbar, HTML display

### Solution Architecture (REST Web API)

ASP.NET Web API is a set of components that simplify HTTP programming, It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as URIs and headers. It is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP and exposes the HTTP programming model to use in HTML, JavaScript, and jQuery.

#### This Solution Architecture
* REST Web API Service call from JQuery
* JQuery AJAX Call to API method **/api/PDFtoHTML/ConvertPDFtoHTMLAndView**
* At Server Side PDF file process to generate HTML from PDF using [Aspose.Pdf API for .NET](http://www.aspose.com/.net/pdf-component.aspx).
* Web API returns generated HTML to Client. 
* Client Browser renders the generated HTML to display out put.

[View REST Web API Architecture](http://s30.postimg.org/vb19lt0y9/RESTWeb_APIArchitecture.png)

![REST Web API Architecture](http://s30.postimg.org/vb19lt0y9/RESTWeb_APIArchitecture.png)

### JQuery Code
    <script type="text/javascript">

        $(document).ready(function () {

            $('#btnUploadFile').on('click', function () {

                // jquery Progress bar function. 
                $("#progressbar").progressbar({ value: 0 });
                var progressbar = $("#progressbar");

                progressbar.progressbar({
                    value: false,
                    complete: function () {
                        progressLabel.text("Complete!");
                    }
                });
                document.getElementById('product').innerHTML = '';
                var data = new FormData();

                var files = $("#fileUpload").get(0).files;

                // Add the uploaded image content to the form data collection
                if (files.length > 0) {
                    data.append("UploadedPDF", files[0]);
                }
                // Make Ajax request with the contentType = false, and procesDate = false
                var ajaxRequest = $.ajax({
                    type: "POST",
                    url: "http://localhost:5879/api/PDFtoHTML/ConvertPDFtoHTMLAndView",
                    contentType: false,
                    processData: false,
                    data: data
                });

                ajaxRequest.done(function (responseData, textStatus) {
                    if (textStatus == 'success') {
                        if (responseData != null) {
                            if (responseData.Key) {
                                $("#fileUpload").val('');
                                document.getElementById('product').innerHTML = responseData.Value;
                                $("#progressbar").progressbar({ value: 100 });
                            } else {
                                $('#product').text(responseData.Value);
                            }
                        }
                    } else {
                        $('#product').text(responseData.Value);
                    }
                });
            });
        });
    </script>

[View PDF to HTML Converter](http://s17.postimg.org/r8xo8ysz3/PDFto_HTML.png)

![PDF to HTML Converter](http://s17.postimg.org/r8xo8ysz3/PDFto_HTML.png)

### System Requirements
In order to setup Web API PDF to HTML Converter using Aspose.Pdf & JQuery solution you need to have the following requirements met:
You need to have the following installed in order to open and extend the source code
* Microsoft Visual Studio 2012 OR higher
* Microsoft .Net Framework 4.0/4.5
* Microsoft MVC 4
* Microsoft Web API 2.2
* [Aspose.Pdf API for .NET](http://www.aspose.com/.net/pdf-component.aspx).

**Note:** We recommend [NuGet](https://docs.nuget.org/consume/installing-nuget) for Microsoft Visual Studio 2012/+, that will automatically load all dependencies [Nuget Installation for Visual Studio](https://docs.nuget.org/consume/installing-nuget).

### Configure & Run Solution
Please follow these simple steps to get started.
* Download/Clone the source code [Download](https://github.com/MRizwanKhan/PDF_TO_HTML_ASPOSE_JQUERY).
* Open Visual Studio 2012/+ and Choose File > Open Project.
* Browse to the latest source code that you have downloaded and open e.g **PDFtoHTMLConverter.sln**.
* Build project "Debug > Start Debuging".
