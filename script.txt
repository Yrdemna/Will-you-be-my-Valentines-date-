// script.js
function playMusic() {
    let music = document.getElementById('bg-music');
    if (music.paused) {
        music.play().catch(error => console.log('Autoplay prevented:', error));
    }
}

document.getElementById('play-music-button').addEventListener('click', function() {
    let music = document.getElementById('bg-music');
    if (music.paused) {
        music.play().catch(error => console.log('Autoplay prevented:', error));
    }
});

function selectOption(option) {
    if (option === 'yes') {
        document.getElementById('question').style.display = 'none';
        document.getElementById('celebratory-text').style.display = 'block';
        displayCatHeart();
        startFloatingHearts();
    } else if (option === 'no') {
        document.getElementById('no-button').innerText = 'You sure?'; 
        let yesButton = document.getElementById('yes-button');
        let currentFontSize = window.getComputedStyle(yesButton).getPropertyValue('font-size');
        let newSize = parseFloat(currentFontSize) * 2;
        yesButton.style.fontSize = newSize + 'px';
    } else {
        alert('Invalid option!');
    }
}

function displayCat() {
    let imageContainer = document.getElementById('image-container');
    let catImage = new Image();
    catImage.src = 'cat.gif';
    catImage.alt = 'Cat';
    catImage.onload = function() {
        imageContainer.appendChild(catImage);
    };
}

displayCat();

function displayCatHeart() {
    document.getElementById('image-container').innerHTML = '';
    let imageContainer = document.getElementById('image-container');
    let catHeartImage = new Image();
    catHeartImage.src = 'cat-heart.gif';
    catHeartImage.alt = 'Cat Heart';
    catHeartImage.onload = function() {
        imageContainer.appendChild(catHeartImage);
        document.getElementById('options').style.display = 'none';
    };
}

function startFloatingHearts() {
    setInterval(() => {
        let heart = document.createElement('div');
        heart.innerHTML = '❤️';
        heart.classList.add('floating-heart');
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.animationDuration = (Math.random() * 2 + 3) + 's';
        document.body.appendChild(heart);
        setTimeout(() => { heart.remove(); }, 5000);
    }, 300);
}

function playMusic() {
    let music = document.getElementById('bg-music');
    if (music.paused) {
        music.play().catch(error => console.log('Autoplay prevented:', error));
    } else {
        music.pause();
        music.currentTime = 0;
    }
}

document.getElementById('play-music-button').addEventListener('click', function() {
    playMusic();
});

// Ensure the button remains interactive and doesn't change behavior
window.addEventListener('load', function() {
    let music = document.getElementById('bg-music');
    let button = document.getElementById('play-music-button');
    button.disabled = false;
    music.volume = 1.0; // Ensure full volume
    document.body.addEventListener('click', function() {
        if (music.paused) {
            music.play().catch(error => console.log('Autoplay prevented:', error));
        }
    }, { once: true }); // Allow user interaction to enable playback
});
