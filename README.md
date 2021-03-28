# Snowpack + TypeScript + React + Tailwind CSS

Just another template.

## How to recreate this?

```bash
export PROJECT_NAME=<INSERT_NAME_HERE>

npx create-snowpack-app $PROJECT_NAME --template @snowpack/app-template-react-typescript
cd $PROJECT_NAME

npm install -D @snowpack/plugin-postcss postcss postcss-cli
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest

npx tailwindcss init -p

rm src/App.css
rm src/logo.svg

cat > src/index.css <<EOF
@tailwind base;
@tailwind components;
@tailwind utilities;
EOF

cat > src/App.tsx <<EOF
import React from 'react';

export default function App() {
  return (
    <div className="font-bold">Welcome to the template! It's super simple!</div>
  );
}
EOF

cat > src/App.test.tsx <<EOF
import * as React from 'react';
import { render } from '@testing-library/react';
import { expect } from 'chai';
import App from './App';

describe('<App>', () => {
  it('renders renders', () => {
    const { getByText } = render(<App />);
    const linkElement = getByText(/template/i);
    expect(document.body.contains(linkElement));
  });
});
EOF

# add @snowpack/plugin-postcss
sed "s/'@snowpack\/plugin-typescript',/'@snowpack\/plugin-typescript',\n    '@snowpack\/plugin-postcss',/" snowpack.config.js | tee snowpack.config.js
```

## Available Scripts

### npm start

Runs the app in the development mode.
Open http://localhost:8080 to view it in the browser.

The page will reload if you make edits.
You will also see any lint errors in the console.

### npm run build

Builds a static copy of your site to the `build/` folder.
Your app is ready to be deployed!

**For the best production performance:** Add a build bundler plugin like "@snowpack/plugin-webpack" to your `snowpack.config.js` config file.

### npm test

Launches the application test runner.
Run with the `--watch` flag (`npm test -- --watch`) to run in interactive watch mode.
