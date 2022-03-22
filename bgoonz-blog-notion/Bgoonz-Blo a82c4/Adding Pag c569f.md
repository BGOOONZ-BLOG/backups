# Adding Page Metadata | Gatsby

[https://www.gatsbyjs.com/docs/add-page-metadata/](https://www.gatsbyjs.com/docs/add-page-metadata/)

![gatsby.jpg](Adding%20Pag%20c569f/gatsby.jpg)

If you've run an [audit with Lighthouse](https://www.gatsbyjs.com/docs/how-to/performance/audit-with-lighthouse/), you may have noticed a lackluster score in the "SEO" category. Let's address how you can improve that score.

Adding metadata to pages (such as a title or description) is key in helping search engines like Google understand your content, and decide when to surface it in search results.

[React Helmet](https://github.com/nfl/react-helmet) is a package that provides a React component interface for you to manage your [document head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

Gatsby's [react helmet plugin](https://www.gatsbyjs.com/plugins/gatsby-plugin-react-helmet/) provides drop-in support for server rendering data added with React Helmet. Using the plugin, attributes you add to React Helmet will be added to the static HTML pages that Gatsby builds.

## Using `React Helmet` and `gatsby-plugin-react-helmet`

1. Install both packages:

```
npm install gatsby-plugin-react-helmet react-helmet
```

1. Add the plugin to the `plugins` array in your `gatsby-config.js` file.

```
  plugins: [`gatsby-plugin-react-helmet`]
```

1. Use `React Helmet` in your pages:

```
import React from "react"import { Helmet } from "react-helmet"class Application extends React.Component {render() {return (<div className="application"><meta charSet="utf-8" /><title>My Title</title><link rel="canonical" href="http://mysite.com/example" /></Helmet></div>
```

> 💡 The above example is from the React Helmet docs. Check those out for more!
> 

You may also be interested in checking out the doc on [adding an SEO component](https://www.gatsbyjs.com/docs/add-seo-component/).
