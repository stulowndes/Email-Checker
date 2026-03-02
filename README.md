# HTML Email UTM Checker

A standalone, single-file HTML app for validating and editing UTM tracking parameters and alt text in HTML emails. No installation required - just open in your browser!

## Features

✅ **No Installation Required** - Open `index.html` in any modern browser  
✅ **Drag & Drop Support** - Simply drag your HTML email file into the app  
✅ **UTM Parameter Validation** - Ensures all links have consistent tracking parameters  
✅ **Duplicate Detection** - Warns when utm_content or alt text values are duplicated  
✅ **Inline Editing** - Edit utm_content for links and alt text for images  
✅ **Auto-conversion** - Alt text automatically converts to kebab-case for utm_content  
✅ **Export Modified HTML** - Download your corrected email with all changes applied

## How to Use

### 1. Open the App
Simply open `index.html` in your browser (Chrome, Firefox, Safari, or Edge).

### 2. Load Your HTML Email
- **Drag & Drop**: Drag your HTML email file onto the drop zone
- **Or Click**: Click the drop zone to browse and select your file

### 3. Review Validation Results

The app will analyze your email and show:

#### Validation Summary
- **Expected UTM Parameters**: Shows and allows editing of canonical values for utm_source, utm_medium, and utm_campaign
- **Update All Links button**: Appears when you modify expected values - applies changes to all links and image links
- **Issues Summary**: Shows total counts of links and images with issues (not individual warnings)

#### Text Links Table
Shows all text-based links (excludes image-only links):
- **URL**: Editable field - change the URL and UTM parameters will be re-parsed automatically
- **utm_source, utm_medium, utm_campaign**: Must match across all links
- **utm_content**: Must be unique for each link (editable)
- **Issues**: Shows specific validation problems for each link

#### Images Table
Shows all images (including those wrapped in links):
- **Alt Text**: Editable field for image descriptions
- **Link URL**: Editable field - if image is wrapped in a link, you can edit the URL here
- **utm_content**: Automatically generated from alt text in kebab-case
- **Issues**: Shows specific validation problems for each image (including parent link UTM mismatches)

### 4. Edit Content
- Click any utm_content or alt text field to edit
- **Edit URLs directly** - Change the full URL in text links or image link fields
  - UTM parameters are automatically re-parsed from the new URL
  - Validation runs immediately after URL changes
- Changes validate in real-time (300ms debounce for text fields)
- Alt text converts automatically: "Shop Now!" → "shop-now"- URL changes trigger immediate re-validation

### 5. Export
Click the **"Export HTML"** button to download your corrected email with all changes applied.

## Validation Rules

### Required UTM Parameters
All links should have:
- `utm_source` (e.g., "newsletter")
- `utm_medium` (e.g., "email")
- `utm_campaign` (e.g., "spring2024")
- `utm_content` (e.g., "shop-now-button")

### Matching Rules
- **utm_source, utm_medium, utm_campaign**: Must be identical across ALL links
- **utm_content**: Must be unique for each link (no duplicates)

### Alt Text Rules
- All images should have descriptive alt text
- Alt text should be unique to avoid duplicate utm_content
- For image links, alt text is converted to utm_content automatically

### Conversion Rules
Alt text to utm_content conversion follows kebab-case:
- Lowercase all letters
- Replace spaces with hyphens
- Remove special characters
- Example: "Shop Now!" → "shop-now"

## Testing

A sample email file (`sample-email.html`) is included with various scenarios:
- ✅ Valid links with complete UTM parameters
- ⚠️ Links with mismatched utm_medium
- ⚠️ Links missing utm_content
- ⚠️ Links completely missing UTM parameters
- ⚠️ Images without alt text
- ⚠️ Duplicate utm_content values
- ⚠️ Duplicate alt text (would create duplicate utm_content)

**Try editing:**
- Change a link URL to add/modify UTM parameters
- Edit canonical UTM values to update all links at once
- Modify alt text and see utm_content update automatically
- Edit image link URLs to fix mismatched parameters

## Browser Compatibility

Works in all modern browsers:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)

**No server required** - runs entirely offline in your browser.

## Technical Details

- **Single File**: Everything is embedded in `index.html` (CSS + JavaScript)
- **No Dependencies**: Uses only browser-native APIs
- **Secure**: HTML parsing uses DOMParser (sandboxed, no script execution)
- **File Size**: ~50KB uncompressed

### Technologies Used
- HTML5 FileReader API for file handling
- DOMParser for safe HTML parsing
- URL and URLSearchParams for UTM parameter extraction
- XMLSerializer for HTML export
- Vanilla JavaScript (no frameworks)

## File Structure

```
Email Checker/
├── index.html          # Main application (single file app)
├── sample-email.html   # Sample HTML email for testing
└── README.md           # This file
```

## Keyboard Shortcuts

- **Ctrl/Cmd + O**: Focus file input (when drop zone is visible)

## Privacy & Security

- **100% Local**: All processing happens in your browser
- **No Data Sent**: No network requests, no tracking, no data collection
- **Safe Parsing**: Uses DOMParser which prevents script execution
- **Offline**: Works without an internet connection

## Troubleshooting

### File Won't Load
- Ensure file extension is `.html` or `.htm`
- Check that the file is a valid HTML document
- Try opening the file in a text editor to verify contents

### Changes Not Saving
- Click the "Export HTML" button to download the modified file
- Original file is never modified (read-only)

### Validation Warnings
- **Missing UTM Parameters**: Add the required parameters to all links
- **Mismatched Parameters**: Ensure all links use the same utm_source, utm_medium, and utm_campaign
- **Duplicate utm_content**: Make each utm_content value unique
- **Missing Alt Text**: Add descriptive alt text to all images

## License

This project is free to use and modify as needed.

## Support

For issues or questions, please check that:
1. You're using a modern browser
2. The HTML file is valid
3. You've reviewed the validation rules above

---

**Version**: 1.0.0  
**Last Updated**: March 2026
