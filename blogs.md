---
title: "Blogs"
layout: layout
---
<!-- The Sidebar is based on W3 school's template: https://www.w3schools.com/w3css/tryit.asp?filename=tryw3css_sidebar_shift -->
<!-- Had a bit of help from Claude for formatting and filter select highlight-->
<div class="w3-sidebar w3-bar-block w3-card w3-animate-left" style="display:none" id="mySidebar">
    <button class="w3-bar-item w3-button w3-large"
    onclick="w3_close()">Close &times;</button>
    <div class="w3-container">
        <div style="display: flex; margin-bottom: 1rem; flex-wrap: wrap;">
            <input type="text" placeholder="Search in blogs... " id="query"
                style="flex: 1; padding: 8px; border: 1px solid #ccc; border-radius: 4px; height: 40px;">
            <button type="submit" id="blog-search-button"
                    style="width: 40px; height: 40px; border-radius: 4px; display: flex; align-items: center; justify-content: center; padding: 0;">
                <i class="fa fa-search" style="font-size: 20px;"></i>
            </button>
            <br>
        </div>
        Photography Type
        <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="digital">
            <label class="form-check-label" for="digital">
                Digital
            </label>
        </div>
        <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="film">
            <label class="form-check-label" for="film">
                Film
            </label>
        </div>
    </div>
</div>

<div id="main" class="page-content">
    <div class="w3-container">
        <h1>Blogs</h1>
        <div class="d-flex align-items-center my-4">
            <button id="openNav" class="w3-button w3-xlarge" title="Blogs filter" onclick="w3_open()">&#9776;</button>
            <h3>Latest Posts</h3>
        </div>
    </div>

    <div class="w3-container">
        <div class="row">
            {% for post in site.posts %}
                <div class="col-md-4 mb-4 blog-card" data-category="{{ post.categories }}">
                    <div class="card">
                    <img src="{{ post.image }}" class="card-img-top" alt="{{ post.title }}">
                        <div class="card-body">
                            <h4 class="card-title">{{ post.title }}</h4>
                            <p class="card-text">{{ post.description }}</p>
                            <div class="full-content" data-full-content="{{ post.content | strip_html | escape }}"></div>
                            <span class="badge bg-info">{{ post.categories }}</span>
                            <a href="{{ post.url | relative_url }}" class="btn btn-primary">Read More</a>
                        </div>
                    </div>
                </div>
            {% endfor %}
        </div>
    </div>
</div>


<script>
    // W3 school's sidebar template
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

    // Obtain header height so the filter sidebar can be adjusted inline with content
    const header = document.querySelector('header');
    const headerHeight = header ? header.offsetHeight : 0;
    console.log('Header height:', headerHeight + 'px');


    // had help from Claude with filter function
    function filterBlogs() {
        const digitalChecked = document.getElementById('digital').checked;
        const filmChecked = document.getElementById('film').checked;
        const blogCards = document.querySelectorAll('.blog-card');

        // Learned this syntax with Claude
        blogCards.forEach(card => {
            const category = card.getAttribute('data-category');
            let showCard = false;

            // Show all cards if no category selected
            if (!digitalChecked && !filmChecked) {
                showCard = true;
            }
            // Show card if card category matches checked category
            else if (digitalChecked && category == 'digital') {
                showCard = true;
            }
            else if (filmChecked && category == 'film') {
                showCard = true;
            }

            if (showCard) {
                card.classList.remove('hidden');
            }
            else {
                card.classList.add('hidden');
            }
        });
    }

    document.addEventListener('DOMContentLoaded', function() {
        document.getElementById('digital').addEventListener('click', filterBlogs);
        document.getElementById('film').addEventListener('click', filterBlogs);

        filterBlogs();
    });


    // Blog search function - a bit of help from claude
    function blogSearch() {
    const query = document.getElementById('query').value.toLowerCase().trim();
    const blogCards = document.querySelectorAll('.blog-card');

    blogCards.forEach(card => {
        // Get all text content from the card
        const cardText = card.textContent.toLowerCase();

        // Claude for these two variables
        const fullContentElement = card.querySelector('[data-full-content]');
        const fullContent = fullContentElement ? fullContentElement.getAttribute('data-full-content').toLowerCase() : '';

        // Check if query matches any content in the card
        if (cardText.includes(query) || fullContent.includes(query)) {
            card.classList.remove('hidden');
        } else {
            card.classList.add('hidden');
        }
    });
}

    //  EventListeners for the searchbar
    document.addEventListener('DOMContentLoaded', function() {
        const searchInput = document.getElementById('query');
        const searchButton = document.getElementById('blog-search-button');

        // Search on button click
        searchButton.addEventListener('click', function(e) {
            e.preventDefault();
            blogSearch();
        });

        // Search on Enter key press
        searchInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                e.preventDefault();
                blogSearch();
            }
        });

        // Real-time search as user types
        searchInput.addEventListener('input', function() {
            blogSearch();
        });
    });

</script>

