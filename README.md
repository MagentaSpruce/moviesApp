# moviesApp
An interactive movies app built using HTML, CSS, & JavaScript. This project also utilizes a movie API().

This project created an interactive movies app which can be cross utilized across projects with minimal edits required.

Building this project has helped me to better learn and practice the following:
1) Working with API's - check script.js for APIKEY, APIURL, and others.
2) Using async/await
3) DOM manipulation
4) Developing and implementing logic


A general walkthrough of the JavaScript code is given below.

First create the getMovies() function.
```JavaScript
async function getMovies(url){
    const resp = await fetch(url);
    const respData = await resp.json();

    showMovies(respData.results)
}
```

Create the getClassByRate() function which will color-coordinate the ratings based on the total ratings average.
```JavaScript
function getClassByRate(vote){
    if(vote > 8){
        return 'green';
    } else if (vote >= 5){
        return 'yellow';
    } else {
        return 'red';
    }
}
```

Add an event listener to the form for setting up the search bar functionality.
```JavaScript
form.addEventListener('submit', (e) => {
    e.preventDefault();

        const searchTerm = search.value;

        if(searchTerm){
            getMovies(SEARCHAPI + searchTerm)

            search.value = '';
        }
});
```

Create the showMovies() function to show the results from user queries.
```JavaScript
function showMovies(movies){
    //clear main
    main.innerHTML = '';
    movies.forEach((movie) => {
        const { poster_path, title, vote_average, overview } = movie;
        const movieEl = document.createElement('div');
        movieEl.classList.add('movie');
        movieEl.innerHTML = `
       
                <img src="${IMGPATH + poster_path}" alt="${title}">
             <div class="movie-info">
                <h3>${title}</h3>
                <span class="${getClassByRate(vote_average)}">${vote_average}</span>
            </div>
            <div class="overview">
            <h4>Movie summary:</h4>
            ${overview}</div>
        `;
        main.appendChild(movieEl);
    });
}
```

***End walkthrough.
