# Enabling Certificates in Open-Edx (Quince)

The Open edX platform is the open-source software whose development led to the creation of the edX organization.

### 1. Go to your admin panel of lms and search for 'switches' then add the followin switch and active it

```bash
    certificates.auto_certificate_generation
```
#### Note: Don't forget to active the switch



### 2. Find "modes" and create a mode for that appropriate course in admin panel.

- Supportedd modes for course-certificates

```bash
        'verified',
        'honor',
        'audit',
        'professional',
        'no-id-professional',
        'masters',
        'executive-education',
        'paid-executive-education',
        'paid-bootcamp',
```

### 3. Enter the cms panel of your site and click on Settiings > Certificates.
-   Enter the details
    - Certificate Details
    - Certificate Signatories

### 4. From right-top corner select the mode form dropdown and click on activate button to active the certificate(You can preview it by clicking on preview button).

## Custom certificate for a perticuler course.

1. Enable these two features to true.

```bash
CUSTOM_CERTIFICATE_TEMPLATES_ENABLED = true
ORGANIZATIONS_APP = true
```
2. go to admin panel of lms and search for "Certificate templates" and add a template for certificate.

- here's the example of template (code):

```bash
<%page expression_filter="h"/>
<%namespace name='static' file='/static_content.html'/>
<%! from django.utils.translation import gettext as _%>
<%
from django.utils.translation import get_language_bidi
dir_rtl = 'rtl' if get_language_bidi() else 'ltr'
course_mode_class = course_mode if course_mode else ''
%>
<!DOCTYPE html>
<html class="no-js" lang="${LANGUAGE_CODE}">
	<head dir="${dir_rtl}">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>${document_title}</title>
	<style>
	
        strong, span, b {
            color: #15457b !important;
        }

		* {
			box-sizing:border-box;
		}
		body {
			color:#000000;
            font-family: Roboto Condensed !important;
			font-size:18px;
		}
		div.system-banner-wrapper {
			-webkit-font-smoothing: antialiased;
			background-color:#000000;
			color:#ffffff;
			font-family: Roboto Condensed !important;
			font-size:1rem;
			margin-bottom:30px;
			padding:20px 0;
		}
		div.system-banner-wrapper > div {
			display:block;
			margin:0 auto;
			width:800px;
		}
		div.system-banner-wrapper > div > h2 {
			font-size:1.125rem;
			font-weight:600;
			line-height:1.6;
			margin-bottom:0.625rem;
		}
		div.system-banner-wrapper span.icon.print:before {
			content:"\f02f";
		}
		div.system-banner-wrapper button {
			-webkit-appearance: button;
			border-color:#0075b4;
			background:#ffffff;
			border:1px solid #ffffff;
			border-radius: 3px;
			color:#0075b4;
			cursor:pointer;
			font-size:0.875rem;
			font-weight:600;
			overflow:visible;
			padding:0.625rem 0.625rem;
			text-transform:none;
		}
		div.system-banner-wrapper button.inverse {
			border-color:#f2f8fb;
			background: transparent;
			color: #f2f8fb;
		}
		div.system-banner-wrapper button.inverse:hover {
			background-color:#ffffff;
			color:#000000;
		}
div.certificate-wrapper {
            border: 2px solid #15457b !important;
            display: block;
            height: 804px;
            margin: 0 auto;
            position: relative;
            width: 1200px !important;
}
		div.certificate-wrapper > header {
            display: block;
            height: 272px;
            position: relative;
            width: 100% !important;
            margin: 0px !important;
		}
		div.certificate-wrapper > header::after {
			clear:both;
			content:"";
			display:block;
			position:relative;
		}
		
		
        div.certificate-wrapper > main > h1 {
            display: block;
            min-height: 50px;
            padding: 5px 17px;
            text-align: center;
            color: #15457b !important;
            font-weight: bold;
            font-size: 19px;
            margin-top: 0px;
		}
		div.certificate-wrapper > main > div.course-name,
		div.certificate-wrapper > main > div.course-period,
		div.certificate-wrapper > main > div.course-provider {
			color:#0e5479;
			display:block;
			line-height:1.3;
			margin-top:15px;
			position:relative;
			text-align:center;
		}
		div.certificate-wrapper > main > div.course-badge {
			display:block;
			height:100px;
			margin:20px 0;
			text-align:center;
		}
		div.certificate-wrapper > main > div.course-badge > img {
			height:100%;
		}
		div.certificate-wrapper > main > div.accomplishment-details {
			font-size:14px;
			line-height:1.3;
			position:relative;
			text-align:center;
		}
		div.certificate-wrapper > main > div.accomplishment-details > span.learner-name {
			display:block;
			font-weight:bold;
			margin:10px 0;
			position:relative;
			text-align:center;
		}
		div.certificate-wrapper > main > div.certificate-date {
			display:block;
			font-size:14px;
			line-height:1.3;
			margin-top:10px;
			position:relative;
			text-align:center;
		}
		div.certificate-wrapper div.signatures {
			display: block;
            position: relative;
            padding-bottom: 10px;
            text-align: center;
            margin: auto 0 !important;
            width: 100% !important;
		}
		div.certificate-wrapper div.signatures::after {
			clear:both;
			content:"";
			display:block;
		}
		div.certificate-wrapper div.signatures div.signature {
			display: inline-block;
            text-align: center;
            width: 50%;
            padding: 10px;
		}
		div.certificate-wrapper div.signatures div.signature > img {
			height:55px;
		}
		div.certificate-wrapper div.signatures div.signature > span {
			display:block;
			font-size:10px;
			text-align:center;
			width:100%;
		}
		div.certificate-wrapper footer {
			bottom: 0;
            display: block;
            font-size: 10px;
            left: 0;
            padding: 0px !important;
            position: absolute;
            margin: 0px !important;
            float: left;
            width: 100% !important;
		}
		@media print {    
			div.system-banner-wrapper, div.system-banner-wrapper * {
				display: none!important;
			}
		}
	</style>
<%block name="js_extra">
<%static:js group='certificates_wv'/>
	<script type="text/javascript">
		$(document).ready(function() {
			document.getElementById("action-print-view").addEventListener("click", printView);
		});
		function printView(event) {
			event.preventDefault();
			window.print();
		}
		function popupWindow(url, title, width, height) {
			// popup a window at center of the screen.
			var left = (screen.width/2)-(width/2);
			var top = (screen.height/2)-(height/2);
			var popupWindow = window.open(url, title, 'toolbar=no, location=no, directories=no, status=no, menubar=no, scrollbars=yes, resizable=yes, width='+width+', height='+height+', top='+top+', left='+left);
			popupWindow.opener = null;
			return popupWindow;
		}
	</script>
</%block>
</head>
<body>
	<div class="system-banner-wrapper" style="margin: auto;">
		<div>
			<h2>${accomplishment_banner_opening}</h2>
			<p class="message-copy copy copy-base emphasized">${accomplishment_banner_congrats}</p>
			<div class="message-actions">
				<button class="inverse" id="action-print-view">
					${_("Print Certificate")}
				</button>
			</div>
		</div>
	</div>
	<div class="certificate-wrapper">
		<main style="margin-top: 250px;">
			<h1>Certificate</br>
of achievement</h1>
<p style="text-align: center;max-width: 900px;margin: auto;">
    “This certificate is awarded to ${accomplishment_copy_username} in recognition of their successful completion of Course ${accomplishment_copy_course_name}. Your hard work, dedication, and commitment to learning have enabled you to achieve this milestone, and we are proud to recognize your accomplishment.”</p>   

 <p style="text-align: center;max-width: 900px;margin: auto;">
     
 <span > ${accomplishment_copy_username}</span> </br>
 <strong>
       </br>
			<span class="course-name"><strong>${accomplishment_copy_course_name}</strong></span>
			</strong>
 <br>  <br>
</p>
			% if certificate_data:
			<div class="signatures" style="text-align: center;">
				% for signatory in certificate_data.get('signatories', []):
					% if signatory.get('signature_image_path'):
				<div class="signature">
					<img src="${static.url(signatory['signature_image_path'])}" alt="${signatory['name']}" />
					<span class="signature-name">${signatory['name']}</span>
					<span class="signature-role">${signatory['title']}</span>
					<span class="signature-organization">${signatory['organization']}</span>
				</div>
					% endif
				% endfor
			</div>
			% endif
		</main>
		
</body>
</html>
```

- Click on save and repeat the abot step 3 and 4 and you're ready to go now with your custom certificate....
