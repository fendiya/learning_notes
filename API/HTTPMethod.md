# Below are HTTP URI and its method for development reference

## sample data schemas
```xml
    <books>
        <book id="1">
            <tittle></title>
            <author><author>
            <price></price>  
            <published_date></published_date>                    
            <contents>
                <chapters>
                    <chapter>
                        <sections>
                            <section>
                                <tittle></tittle>
                                <body></body>
                            </section>
                            <section>
                            </section>
                        </sections>
                    </champter>
                    <chapter>
                    </chapter>
                </chapters>
            </contents>
        <book>
        <book>
        </book>
    </books>
```

## to retrieve information from application
### retrieve information
#### retrieve all books 
    URL : http://fendiyaditya.com/books \
    Method : GET \
    BODY : null \
#### retrieve all books and pagiate the result  # PAGING
    URL : http://fendiyaditya.com/books?page=2 \
    Method : GET \
    BODY : null \
#### retrieve all books and sort by author A first (asc), then by published date newer first (desc). (-) means descending # SORTING
    URL : http://fendiyaditya.com/books?sort_by=author,-published_date
    Method : GET \
    BODY : null \
#### retrieve all books where author is fendi  # STATIC FILTERING
    URL : http://fendiyaditya.com/books?author=fendi \
    Method : GET \
    BODY : null \   
#### retrieve all books where author is like fen*  # DYNAMIC FILTERING / searching USE LUCENE/ELASTICSEARCH STYLE
    URL : ?? need to learn more \
    Method : GET \
    BODY : null \ 
#### retrieve all books tittle and author  # DYNAMIC OUTPUT
    URL : http://fendiyaditya.com/books?fields=tittle,author \
    Method : GET \
    BODY : null \
#### retrieve only book with id=1
    URL : http://fendiyaditya.com/books/1 \
    Method : GET \
    BODY : null \
#### retrieve all chapters in book with id=1
    URL : http://fendiyaditya.com/books/book/1/contents/chapters \
    Method : GET \
    BODY : null \

##### Reference : \
1. https://www.moesif.com/blog/technical/api-design/REST-API-Design-Filtering-Sorting-and-Pagination/ \
2. https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
3. https://www.deepcrawl.com/knowledge/technical-seo-library/pagination-seo-guide/