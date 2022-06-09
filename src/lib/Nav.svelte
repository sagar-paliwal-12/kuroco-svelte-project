<nav>
    <img src="https://kuroco-svelte-project.g.kuroco-img.app/files/user/logo.png" height="30" alt="">
    <ul>
        <li>
            <a href="/">Home</a>
        </li>
        <li>
            <a href="/">Services</a>
        </li>
        <li>
            <a href="/">About</a>
        </li>
        <li>
            <a href="/">Enquiry</a>
        </li>
    </ul>
</nav>

<style>
    nav {
        background: #e9af3c;
        padding: 10px;
        display: flex;
        justify-content: space-between;
    }
    img {
        margin-right: 40px;
    }
    ul {
        display: flex;
        list-style: none;
        margin: 0;
        padding: 0;
    }
    li {
        width: 100px;
        letter-spacing: 1px;
        margin-right: 10px;
        font-size: 20px;
        text-decoration-color: #c62828;
    }
    li a {
        color: #c62828;
        text-decoration: none;
    }
    li a:hover {
        color: #000
    }
</style>
