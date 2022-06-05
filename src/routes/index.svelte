<script>
    import photos from "$lib/photos.json";

    function shuffleArray(array) {
        let i = array.length;
        while (i--) {
            const ri = Math.floor(Math.random() * i);
            [array[i], array[ri]] = [array[ri], array[i]];
        }
        return array;
    }

    let isDone = false;
    let finalPhoto = {};

    const photosClone = [...photos];
    let shuffledPhotos = shuffleArray(photosClone)



    let photo1;
    let photo2;
    if(shuffledPhotos.length > 0) {
        photo1 = shuffledPhotos.shift();
        shuffledPhotos = shuffledPhotos;
        photo2 = shuffledPhotos.shift();
        shuffledPhotos = shuffledPhotos;
    }



    const handleChoose = (photoID) => {
        const photoObject = photos.find(item => item.id === photoID);

        shuffledPhotos = [...shuffledPhotos, photoObject];

        console.log(">>>shuffledPhotos", shuffledPhotos)

        photo1 = shuffledPhotos.shift();
        shuffledPhotos = [...shuffledPhotos];
        photo2 = shuffledPhotos.shift();
        shuffledPhotos = [...shuffledPhotos];


        if(shuffledPhotos.length === 1) {
            console.log(">>>>>>> DONE")
            finalPhoto = shuffledPhotos[0];
            isDone = true;
            return false;
        }
    }

</script>

{#if isDone}
    <div class="container">
        <h1 class="py-5">Done!</h1>

        <img src="/images/{finalPhoto.name}" alt="" class="img-fluid" />
    </div>
{:else}
    <div class="container">
        <h1 class="py-5">Pick 1</h1>

        <div class="row">
            <div class="col-md-6">
                <button type="button" on:click={() => {handleChoose(photo1.id)}}>
                    <img src="/images/{photo1.name}" alt="" class="img-fluid" />
                </button>
            </div>

            <div class="col-md-6">
                <button type="button" on:click={() => {handleChoose(photo2.id)}}>
                    <img src="/images/{photo2.name}" alt="" class="img-fluid" />
                </button>
            </div>
        </div>
    </div>
{/if}
