<template>
    <NuxtLink to="/" :class="[$style.logo,{[$style.light]:light}]">
        <svg
          width="50"
          height="50"
          viewBox="0 0 75 75"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          id="logo"
        >
          <g>
            <path
              d="M67.1 75H74.2V1.20001H0.300003V75H49.1L44.7 68.1L7.1 67.9V7.90001H67.2L67.1 75Z"
              fill="#DCDCDC"
            />
            <path
              d="M67.2 75L72.7 70.5L51.2 43.1H42.4L67.2 75Z"
              fill="#DCDCDC"
            />
            <path d="M42.3 75H49.4V43.1H42.5L42.3 75Z" fill="#DCDCDC" />
          </g>
        </svg>
    </NuxtLink>
</template>

<script>
export default {
    props:['light']
}
</script>

<style lang="scss" module>
    .logo{
        &.light{
            path{
                fill:$font-color-l
            }
        }
    }
</style>