# Rhythmix

## Description:
* Rhythmix is a music player built in ReactJS


## User Guideline:
* Go to [Rhythmix](https://murmuring-island-74901.herokuapp.com/)
* Click Collection to select a playlist
* The song on play has a play button in place of the song number to easily keep track
* Includes music controls like forward, pause, skip, playback and volume range


## Setup and Configuration:

### Languages and Frameworks:
* ReactJS Library
* HTML / CSS


## Running the application locally:
* Clone or download the repository
* Run `npm install --save`
* Start the react server using `npm start`
* Run the application through localhost:3000


## Building The App's Features: A summary

 #### The UI 
 
Building out Rhythmix started with making wireframes and designing the landing page. It had to be a landing page where users would know exactly what the site is about, and all the information laid out clearly. The application's UI would have a slogan and three key selling points. Landing.js component was mainly for the look and feel of the application.

#### List of albums for the user to choose from

Library.js component was created to store the list of albums. Each album has a cover image, a title and name of the artist. In production, Library.js would get its data from requests to an API. For this application though, we replicate the response of an API by declaring data in a data/album.js, and import it to Library.js `import albumData from './../data/albums'`. 

In the Library.js component, albumData is assigned to albums `this.state = { albums: albumData }` and use the `map()` array method to convert raw array data into an array of JSX elements that React can render. The `Link` component helps to build a unique path for each album.

          this.state.albums.map((album, index) =>
            <Link to={`/album/${album.slug}`} key={index}>
                <img src={album.albumCover} alt={album.title} />
                <div>{album.title}</div>
                <div>{album.artist}</div>
                <div>{album.songs.length}</div>
            </Link>
          )        

#### Displaying basic album information

The Album.js component will store all the functionality related the albums. I needed to find the `album` object in `albumData` that has the same slug property as `this.props.match.params.slug` so I can set an `album` property to the state. I made use of `find()` array method to retrieve the matching `album` object and assign it to an `album` variable. 
Not forgetting to import `albumData` to Album.js, otherwise, the code won't work, `import albumData from './../data/albums'`.

        const album = albumData.find( album => {
            return album.slug === this.props.match.params.slug
        });

        this.state = {
            album: album
        };


>  In this context, the use of `slug` is a version of the album title that is formatted to work well in a URL and will also serve as a unique identifier for each album

With the above code, I could easily access album data and render to the UI.

        <section id="album-info">
           <img id="album-cover-art" />
           <div className="album-details">
             <h1 id="album-title"></h1>
             <h2 className="artist"></h2>
             <div id="release-info"></div>
           </div>
         </section>


##### Music Controls

To build music control features, like play, pause and volumecontrol, I added HMTL5's `<audio>` element `this.audiElement = document.createElement(‘audio’);`

I also added `currentSong` and `isPlaying` to state to display song data to the screen and whether the song is playing or not.

          this.state = { 
              album: album,
              currentSong: album.songs[0],
              isPlaying: false
            };

To see the complete list of functionality as well as the code, please click [here](https://github.com/Ruby777/rhythmix/blob/master/src/components/Album.js).

#### Listening Experience

Finally, we add a separate component, PlayerBar.js to manage the user's listening experience. Here, we place the `onClick()` and `onChange()` functions to respond to the user's interaction with the Player Bar on the UI e.g. Clicking play, pause, skip etc.


