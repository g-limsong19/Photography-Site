---
title: "Blogs"
layout: layout
---
# Blogs

<div class="w3-container">
    <button class="semi-circle-btn" onclick="toggleSidebar()" id="openNav">></button>
    <div class="w3-container">
        <h3 class="my-4">Latest Posts</h3>
    </div>

    <div class="w3-sidebar w3-bar-block w3-card w3-animate-left" style="display:none" id="mySidebar">
        <a href="#" class="w3-bar-item w3-button">Link 1</a>
        <a href="#" class="w3-bar-item w3-button">Link 2</a>
        <a href="#" class="w3-bar-item w3-button">Link 3</a>
    </div>

    <div id="main">
        <div class="row">
            {% for post in site.posts %}
                <div class="col-md-4 mb-4">
                    <div class="card">
                    <img src="{{ post.image }}" class="card-img-top" alt="{{ post.title }}">
                        <div class="card-body">
                            <h5 class="card-title">{{ post.title }}</h5>
                            <a href="{{ post.url | relative_url }}" class="btn btn-primary">Read More</a>
                        </div>
                    </div>
                </div>
            {% endfor %}
        </div>
</div>


<script>
    document.querySelector('.semi-circle-btn').addEventListener('click', function() {
        if (this.textContent === '>') {
            this.textContent = '<';
        }
        else if (this.textContent === '<') {
            this.textContent = '>';
        }
    })

    let sidebarOpen = false;

    function toggleSidebar() {
        if (sidebarOpen) {
            w3_close();
        } else {
            w3_open();
        }
    }

    function w3_open() {
        document.getElementById("main").style.marginLeft = "25%";
        document.getElementById("mySidebar").style.width = "25%";
        document.getElementById("mySidebar").style.display = "block";
        document.getElementById("openNav").style.display = 'none';
        sidebarOpen = true;

    }
    function w3_close() {
        document.getElementById("main").style.marginLeft = "0%";
        document.getElementById("mySidebar").style.display = "none";
        document.getElementById("openNav").style.display = "inline-block";
        sidebarOpen = false;
    }

</script>

