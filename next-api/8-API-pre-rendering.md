### APIs and Pre-rendering

pages/comments/[commentId].js

```javascript
import { comments } from '../../data/comments'

function Comment({ comment }) {
  return (
    <div>
      {comment.id}. {comment.text}
    </div>
  )
}

export default Comment

export async function getStaticProps(context) {
  const { params } = context
  const { commentId } = params

  const comment = comments.find(comment => comment.id === parseInt(commentId))
  console.log(comment)

  /** Don't do this 
  const response = await fetch(`http:localhost:3000/api/comments/${commentId}`)
  const data = await response.json()
  */

  return {
    props: {
      comment
    }
  }
}

export async function getStaticPaths() {
  return {
    paths: [
      { params: { commentId: '1' } },
      { params: { commentId: '2' } },
      { params: { commentId: '3' } }
    ],
    fallback: false
  }
}
```

We are not advised to call our own api route within the getstatic props or getserversideprops, we can external api but calling our own api route is not recommended. Calling it via url introdcues an additional rount trip which is not necessary.

We have already imported comments array and used it with getstaticprops to find the comment whose id matches the comment id from the url segment.

Exact same logic we had in the api as well.

We should not call api route for pre-rendering.
