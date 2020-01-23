# react-ts-storybook
example React.js component library setup with Storybook MDX Docs and Typescript

This is really just a quick thing I put together as a working example of [my recommendations in this ticket](https://github.com/jaredpalmer/tsdx/issues/440). 

## Steps Taken
- Initialize a new tsdx project using the react-with-storybook template
- At the time of this writing, the template for react-with-storybook for tsdx has not yet been updated to use the new consolidated way to configure Storybook via `main.ts`
    * This was already updated in the project when I checked and it just wasn't released yet
    * So next step was to switch the config to that one `main.ts` configuration file (see commits, changes are very similar to [#435](https://github.com/jaredpalmer/tsdx/pull/435))
- Follow Storybook Docs installation instructions [here](https://www.npmjs.com/package/@storybook/addon-docs#installation)
    * `yarn add -D @storybook/addon-docs react react-is babel-loader`
    * ```javascript
      module.exports = {
        stories: ['../stories/**/*.stories.(tsx|mdx)'],
        addons: ['@storybook/addon-docs'],
      };
      ```
- Install and configure [Storybook TypeScript preset](https://github.com/storybookjs/presets/tree/master/packages/preset-typescript)
    * `yarn add -D @storybook/preset-typescript react-docgen-typescript-loader ts-loader fork-ts-checker-webpack-plugin`
    * ```javascript
      module.exports = {
        stories: ['../stories/**/*.stories.(tsx|mdx)'],
        addons: ['@storybook/addon-docs'],
        presets: [
          {
            name: '@storybook/preset-typescript',
            options: {
              include: [
                path.resolve(__dirname, '../src'),
                path.resolve(__dirname, '../stories'),
              ],
            },
          },
        ],
      };
      ```
  - From here you just need to add an example MDX file, see [Thing.stories.mdx](stories/Thing.stories.mdx)
  - Done! Running `yarn storybook` should open up the docs and you should notice an extra entry there generated from the MDX story



