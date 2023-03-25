### Dynamic API Routes

/api/comments will handle both GET and POST request. However for delete req. our endpoint ->

/api/comments/commentId

from req.query we can extract comment Id.

pages/api/comments/[commentId].js

```javascript
import { comments } from "../../../data/comments";

export default function handler(req, res) {
  const { commentId } = req.query;
  const comment = comments.find(
    (comment) => comment.id === parseInt(commentId)
  );
  res.status(200).json(comment);
}
```
