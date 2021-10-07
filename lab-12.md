# Spring and REST

- Similar to node and install packages
- In java you have to be aware to import dependencies when you use outside libraries and put them into your build.gradle
- Write down postgres password

- application.properties
  - contains your postgres
  - `spring.datasource.url=jdbc:postgresql://localhost:5432/songr` // songr has to match the name of the database you create on pgAdmin
  - `spring.datasource.username=postgres`
  - `spring.datasource.password=password`
  - `spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect`
  - `spring.jpa.show-sql=false`
  - `spring.jpa.hibernate.ddl-auto=update`

## Hibernate

- ORM / Object relational impedance mismatch
- Takes classes and puts it into your database
- Handles SQL without have to know SQL
- annotations
    - @Entity
    - @Id
    - @GeneratedValue
    - Lob
    - Type

## Setting up Database

- In Contoller

```java
@Controller
public class SongrController {

    // Wires up repository
    @Autowired
    AlbumRepository albumRepository;

    @GetMapping("/albums")
    public String albumPage(Model m){
        // Retrieves items from database
        List<Album> dbAlbums = albumRepository.findAll();
        m.addAttribute("albums", dbAlbums);
        return "pages/albums";
    }

    @PostMapping("/")
    public RedirectView createAlbum(String title, String artist, int songCount, int lengthInS, String imageURL){
        Album newAlbum = new Album(title, artist, songCount, lengthInS, imageURL);
        albumRepository.save(newAlbum);
        return new RedirectView("/");
    }
}
```

- @Autowired
- Bring in repository
- `albumRepository.findAll()` goes in to psql and retrieves all from the db
- Redirect retains CRUD method through a redirect

## In Album

```java
// Store in the db
@Entity
public class Album {
    // Add Id and GeneratedValue annotations
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    long id;
    @Lob
    @Type(type = "org.hibernate.type.TextType")
    String title;
    String artist;
    int songCount;
    int lengthInS;
    String imageUrl;

    // JPA and Hibernate NEED Default constructor
    protected Album(){

    }

    public Album(String title, String artist, int songCount, int lengthInS, String imageUrl) {
        this.title = title;
        this.artist = artist;
        this.songCount = songCount;
        this.lengthInS = lengthInS;
        this.imageUrl = imageUrl;
    }

    public String getArtist(){
        return this.artist;
    }
    public String getTitle(){
        return this.title;
    }
    public int getSongCount(){
        return this.songCount;
    }
    public int getLengthInS(){
        return this.lengthInS;
    }
    public String imageUrl(){
        return this.imageUrl;
    }
    public void setImageUrl(String path)
    {
        this.imageUrl = path;
    }
}

```

- CREATE DEFAULT CONSTRUCTOR
- Add annotations
  - @Entity
  - @Id
    - long id;
  - @GeneratedValue(strategy = GenerationType.IDENTITY)

## Creating a Repository

```java
@Repository
public interface AlbumRepository extends JpaRepository<Album, Long> {
    public Album findByArtist(String artist);
}
```

## Linking HTML with Routes

```html
 <form action="/" method="post">
        <fieldset>
            <legend>Add Album</legend>
            <label for="artist"> Artist Name:</label>
            <input type="text" name="artist">
            <label for="title"> Album Title:</label>
            <input type="text" name="title">
            <label for="songCount"> Song Count:</label>
            <input type="text" name="songCount">
            <label for="lengthInS"> Album Length in Seconds:</label>
            <input type="text" name="lengthInS">
            <label for="imageURL"> Image Url:</label>
            <input type="text" name="imageURL">
            <input type="submit" value="Add">
        </fieldset>
    </form>
```

- the `name` attribute in the input tags correlate to properties in the table

```java
    @PostMapping("/")
    public RedirectView createAlbum(String title, String artist, int songCount, int lengthInS, String imageURL){
        Album newAlbum = new Album(title, artist, songCount, lengthInS, imageURL);
        albumRepository.save(newAlbum);
        return new RedirectView("/");
    }
```

- Form frields will be used toward this
- Redirect reopens and gets the hompage