<script>
    import { onMount, onDestroy } from 'svelte';

    let gun;
    let recoilAmount = -20; // Adjust this value to change the recoil distance
    let originalTransform = ''; // Store the original transform property

    function rotateGun(event) {
        // Disable functionality on screens smaller than 640px
        if (!gun || window.innerWidth < 640) return;

        // Get the bounding box of the gun image
        const rect = gun.getBoundingClientRect();

        // Calculate the center of the gun image
        const centerX = rect.left + rect.width / 2;
        const centerY = rect.top + rect.height / 2;

        // Calculate the angle from the center of the gun image to the mouse position
        const angle = Math.atan2(event.clientY - centerY, event.clientX - centerX) * (180 / Math.PI);

        // Apply the rotation
        gun.style.transform = `rotate(${angle}deg)`;
    }

    function handleClick() {
        // Move the gun to the left
        gun.style.transform += ` translateX(${recoilAmount}px)`;

        // Immediately reset to the original position
        setTimeout(() => {
            gun.style.transform = gun.style.transform.replace(/ translateX\([-0-9.]+\px\)/, ''); // Remove the translateX
        }, 10); // No delay, remove translate immediately
    }

    onMount(() => {
        // Attach event listeners to the entire window
        window.addEventListener('mousemove', rotateGun);
        window.addEventListener('click', handleClick);
    });

    onDestroy(() => {
        // Remove event listeners when the component is destroyed
        window.removeEventListener('mousemove', rotateGun);
        window.removeEventListener('click', handleClick);
    });
</script>

<div id="frame-container" class="bg-black flex flex-col justify-center items-center">
    <div class="flex md:-translate-x-60 sm:-translate-x-44 -translate-x-20 z-10">
        <img class="md:w-32 w-24" src="../../public/character.png" alt="CHARACTER">
        <img bind:this={gun} id="gun" class="md:w-20 w-14 object-contain md:-ml-7 -ml-4" src="../../public/gun.png" alt="CHARACTER">
    </div>

    <iframe class="w-[min(1000px,95%)] aspect-video -mt-8 z-20 rounded-xl" src="https://www.youtube.com/embed/0YKjFoGxbec?si=lg02hWlZ9DHzkUEe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

<style>
    #gun {
        transition: transform 0.1s cubic-bezier(0.215, 0.610, 0.355, 1);
    }

    #frame-container {
        background: linear-gradient(to bottom, black 55%, #181818 45%);
    }
</style>
