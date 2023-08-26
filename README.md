<html>
<head>
    <title>Instagram-Like Feature</title>
</head>
<body>
    <h1>Posts</h1>
    <div id="posts"></div>
    
    <script>
        async function likePost(postId) {
            const response = await fetch(`/like/${postId}`, {
                method: 'POST'
            });

            if (response.ok) {
                loadPosts(); // Refresh posts after liking
            } else {
                console.error('Failed to like post');
            }
        }

        async function loadPosts() {
            const response = await fetch('/posts');
            const data = await response.json();

            const postsContainer = document.getElementById('posts');
            postsContainer.innerHTML = '';

            data.posts.forEach(post => {
                const postDiv = document.createElement('div');
                postDiv.innerHTML = `
                    <img src="${post.image_url}" alt="Post Image" style="max-width: 200px;">
                    <p>Likes: ${post.likes}</p>
                    <button onclick="likePost(${post.id})">Like</button>
                `;
                postsContainer.appendChild(postDiv);
            });
        }

        // Load posts on page load
        loadPosts();
    </script>
</body>
</html
