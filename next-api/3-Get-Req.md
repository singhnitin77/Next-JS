### API get Request

data/comment.js

```javascript
export const comments = [
  {
    id: 1,
    text: "This is the first comment",
  },
  {
    id: 2,
    text: "This is the second comment",
  },
  {
    id: 3,
    text: "This is the third comment",
  },
];
```


pages/api/comments/index.js - http://localhost:3000/api/comments

```javascript
import { comments } from "../../../data/comments";

export default function handler(req, res) {
  res.status(200).json(comments);
}
```

pages/comments/index.js

```javascript
import { useState } from "react";

function CommentsPage() {
  const [comments, setComments] = useState([]);
  const fetchComments = async () => {
    const response = await fetch("/api/comments");
    const data = await response.json();
    setComments(data);
  };

  return (
    <>
      <button onClick={fetchComments}>Load comments</button>
      {comments.map((comment) => {
        return (
          <div key={comment.id}>
            {comment.id} {comment.text}
          </div>
        );
      })}
    </>
  );
}

export default CommentsPage;
```
