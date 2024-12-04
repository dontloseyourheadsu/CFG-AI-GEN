# CFG AI Generator

A web application that validates Context-Free Grammar (CFG) expressions using AI-generated rules and compares them against predefined grammar patterns. The app specializes in validating arithmetic expressions and provides detailed feedback on syntax and grammar compliance.

## Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/download)
- [Live Server Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- A modern web browser (Chrome, Firefox, Safari, or Edge)
- [Git](https://git-scm.com/downloads) (for cloning the repository)
- An Eden AI API key (for AI-powered validation)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/dontloseyourheadsu/CFG-AI-GEN.git
cd CFG-AI-GEN
```

2. Create a `config.js` file in the root directory with your Eden AI bearer token:
```javascript
// config.js
const CONFIG = {
    API_URL_POST: "https://api.edenai.run/v2/workflow/48116924-110e-42e0-81bd-eec91f45ec92/execution/",
    API_URL_GET_TEMPLATE: "https://api.edenai.run/v2/workflow/48116924-110e-42e0-81bd-eec91f45ec92/execution/{id}/",
    BEARER_TOKEN: "Bearer your_token_here",
    POLLING_INTERVAL: 5000
};

export default CONFIG;
```

3. Update the `index.html` file to import the configuration:
```html
<!-- Add this before the existing script tag -->
<script type="module">
    import CONFIG from './config.js';
    // Your existing script content here
</script>
```

## Running the Application

1. Open the project in Visual Studio Code:
```bash
code .
```

2. Start Live Server:
   - Right-click on `index.html` in VS Code's file explorer
   - Select "Open with Live Server"
   - The application should open in your default web browser at `http://127.0.0.1:5500`

## Usage

1. Enter arithmetic expressions in the text area, one per line. Examples:
```
2 + 3 * 4
(a + b) * c
x * (y - z) / w
```

2. Click the "Validate CFG" button to analyze your expressions.

3. Review the results:
   - Syntax validation shows if expressions are properly formatted
   - CFG comparison displays how AI-generated rules match predefined patterns
   - Raw AI response shows the complete grammar generation output

## Features

- **Syntax Validation**: Checks for:
  - Balanced parentheses
  - Proper operator placement
  - Valid token sequences
  - Empty expressions
  - Consecutive operators

- **CFG Analysis**: Compares AI-generated grammar rules against hardcoded patterns for:
  - Expression rules (`expr`)
  - Term rules (`term`)
  - Factor rules (`factor`)

- **Visual Feedback**:
  - Color-coded results (green for matches, red for mismatches)
  - Detailed error messages
  - Side-by-side comparison of expected and actual grammar rules

## Development

### Project Structure
```
CFG-AI-GEN/
├── index.html       # Main application file
├── config.js        # Configuration file (create this)
├── README.md        # Documentation
└── .gitignore      # Git ignore file
```

### Configuration

The `config.js` file contains sensitive information and should not be committed to the repository. Add it to `.gitignore`:
```
# .gitignore
config.js
```

### Modifying the Grammar

To modify the hardcoded grammar rules, update the `HARDCODED_CFG` object in the JavaScript code:
```javascript
const HARDCODED_CFG = {
    arithmetic: {
        productions: [
            { left: "expr", right: ["expr + term", "expr - term", "term"] },
            { left: "term", right: ["term * factor", "term / factor", "factor"] },
            { left: "factor", right: ["( expr )", "number", "identifier"] }
        ]
    }
};
```

## Troubleshooting

1. **CORS Issues**: If you encounter CORS errors:
   - Ensure you're using Live Server
   - Check that your Eden AI API key is valid
   - Verify the API endpoints in your configuration

2. **Syntax Validation Errors**: Common issues:
   - Missing spaces between operators and operands
   - Unmatched parentheses
   - Invalid operator sequences

3. **AI Response Timeout**: If the AI response takes too long:
   - Check your internet connection
   - Verify your API key permissions
   - Adjust the `POLLING_INTERVAL` in `config.js`

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support, please open an issue in the GitHub repository or contact the maintainers directly.
