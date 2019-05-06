## Using local file system
The folder blog_test contains a basic gatsby site that is able to build a blog from markdown files.

This is made possible by the configuration in the file [here](./blog_test/gatsby-config.js)

The following:

    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `pages`,
        path: `${__dirname}/src/pages`
      }
    }

uses a source plugin (gatsby-source-filesystem) to allow the querying of data from the file system as well as transformer plugin (gatsby-transformer-remark) to allow the specific structure in the markdown to be parsed as data.

This allows things such as:

   
     ---
     path: "/third-post"
     date: "2018-07-23"
     title: "Post C"
     tags: ['this', 'other']
     excerpt: "A look at post 3"
     ---

to be queried in the [index.js](./blog_post/pages/index.js) like so:

`
{
    allMarkdownRemark(
      sort: {order: DESC, fields: [frontmatter___date]}
    ) {
      edges {
        node {
          frontmatter {
            title
            path
            date
          }
        }
      }
    } 
  }
`

The index.js file is by convention the root of the site.

## Using an external data source

The following [app](./using-wordpress) is lifted from the Gatsby repo.  This is an example of an app using an external data source (wordpress cms).  It has an example of a gatsby-node.js file which is the file that one creates to do create more complex pages based of a given datasource / transformer.

## Notes
Gatsby will build a site based of a given data source.

### Main use case
Once the site is built changes to the underlying data store such as a cms will not be reflected in the site that was built unless further React development is done, though at this point there would be no real benifit to using Gatsby.

### Other benefits
For sites that need an extremely fast time to first render Gatsby offers the ability to serve static files (faster than dynamic server generated content) along with React components that can be interacted with after the initial page has loaded.

#### Preloading and fetching
The Gatsby repo has a great example [here](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-prefetching-preloading-modules) of how to prefetch and preload modules.

More info on how to set this up in webpack can be found [here](https://webpack.js.org/guides/code-splitting/#prefetchingpreloading-modules).

The react docs website is an amazing example of a fully optimized Gatsby site.