<template>
  <div class="container">
    <div class="row">
      <div
        v-for="(product, index) in products"
        :key="'product-' + index"
        class="col-md-4"
      >
        <div class="card mb-3">
          <img :src="product.photoURL" class="card-img-top" />
          <div class="card-body">
            <h5 class="card-title">
              {{ product.name }}
            </h5>
            <p class="card-text">
              {{ product.description }}
            </p>
            <div class="d-grid">
              <button
                class="btn btn-outline-primary"
                @click="addToCart(product)"
              >
                Add to cart
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Add the shopping cart here! 👀✌️ -->
    <ShoppingCart v-model="shoppingCart" />
  </div>
</template>

<script lang="js">
export default {
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Camera Model 1',
          description: 'Lorem ipsum dolor sit amet.',
          price: 950,
          photoURL: 'https://t1.daumcdn.net/cfile/tistory/22166E33597DEA7C1B',
        },
                {
          id: 2,
          name: 'Camera Model 2',
          description: 'Lore dolor sit amet.',
          price: 950,
          photoURL: 'http://i1.adis.ws/i/canon/eos-r6-rf24-105mm-f4_7.1_is_stm_front-on_square_6412568cc0e7484b96bd55e43069a56c',
        },
                        {
          id: 3,
          name: 'Camera Model 3',
          description: 'dali',
          price: 950,
          photoURL: 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAoHCBIWFRISFRIYGBIYGBgaFBgYEhESGBgSGBgZGRgYGRgcIS4mHB4rHxgYJjgmLC8xNTU1GiQ7QDs0Py40NTEBDAwMEA8QGBIRGD8jGCE0NDExMTExMTExMTE0MTQxMTQ0MTQ0MTE0NDQ0NDQ0ND80ND8/ND8/NDQxNEA0NDQ/NP/AABEIAOAA4QMBIgACEQEDEQH/xAAcAAEAAgMBAQEAAAAAAAAAAAAABAUCAwYBBwj/xABEEAACAQICBgUHCgUEAgMAAAABAgADEQQhBRIxQVFhBiJxgZETMlKSobHBFCNCYnKCorLR8AdUc5PCJDOz4WPxFVPS/8QAFwEBAQEBAAAAAAAAAAAAAAAAAAECA//EABsRAQEBAQEBAQEAAAAAAAAAAAABMRECIWES/9oADAMBAAIRAxEAPwD7NERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQPJ4Z7KbSmK1m8kpyHnnidy/GWTqVvraSzsgv9Y7O4b5pavUO1yOywmqkk3Wl4nWJB3s3rNMGUDMsbbyWOztmwyp03WsEp7Q5JYXtdVK5X+8PCLeRHv/AMpTLimgZmPm9cJrfZBN28JuXGKGCOHRzsD6wB7DOewWgayYhawQsVYPZnRVNwxChgWOxbZjhL3SWPqVadRHwliDqqxr07a7AFSDa9sxe4G22cz2rxPCjifWMy1frN6xlTobFl0zJup1Tfbla1+4iWiman1Hur9ZvWaNX6zesYiUNX6zesYt9ZvWMTyAsfSb1jGfpN6xi8QBd/Tb1mmPymoNjnvz989M1PA2Lpp089Qy7yuTDnbYfZLjD11dQ6m6nYf3sM5LFb570b0jqV/Ik9SpfV5VAL5doB8BJYsrs4iJloiIgIiICIiAiIga6tQKrMdigk9gF5zOFubsdpJJ7TmZdaae1GpzsvrMAfYZVYNchNeWamIJ6ZxPST+JGEwztRVGr1FNn1WCIrDapc7T2CSei3T7C41/IhWpVyCVRipD2FzqONpAzsbH2x1OOtMotNk+Vw9vr9m1NsuGeVelFvUoff8AeknrCLxKL3W7LtW/UI+huz2ZN63KaK1J9XNltdbgJ9Em+RvtzUd3PKzUZjtHuImspcMOfuMy04zo6erU+2fypOhSc90b2Vv6rD8KTokE35yM1472Kj0iR5yi1lLXz27N3bMPlVOxbXTVFrnXWwJ2AmeYuizeTtbqlibm2RR1HtIkI4J1W+qLhadiKgp6rojBmBII2tv2gmUTRi6d2HlFuou3WFgO3w8RPVxNO1/KLaxN9ZbWBsT2AkZ85FqYWpcsdUt8yQL6odqdy42ZDhNLYSowXJLq71LBgwOs4Kpf0SAc+QgWtonpiBiZqqSJ0ixdSjhsTWpLrVEpsyrYnrAbSBttttynzn+HPSrG4jEvRrVTVRkZySqg0yv0gVA6pNltsuw2bw77FynosRiMORt8qntcAy5xUpKjatSm3ouh8HBgfUIiJhsiIgIiICIiAiIgVenh8195ffKDS2KajhMVWXzko1GX7QQ6vttLvpA/VRd5a/cAb+0ic10uy0djv6D+2wmpjN18gweg9akH8m1RvJ+VqHM6qGxLHgMxc8TKYs1CqlRCQyMrob5gqbgX7p21Gu6Yak1Nyq1MOiPax1kKgOp71t3TidLjrsOCgd9r/GKsfpWioZr7rX8ReQNNizUuNnt+CWGB2j7A/KJX9IFI8lUF7qWAtY9Z9UAnkLE90lxmLbCYoEA39Dxs1/ePGe08UusVvmXAt2t/0fCVGF0vc6lwzHVyVqbManW1sgd9xJor1g1R2otqqxZeqLlBYkdu23bMtdVOgkt5X+q35Ul4sqdCp1Xa1tZyR6qj3g+EtxN+cjN17Ib4MnWtUIJ1s+tlra/P66f2x3TIlEZMPZg2tcXJK52N/KcTwdR9wd3uHw+pbO/URdlr6mtn7fZKaj0uwj1xhl1/KFzTB8mNXXBK8b2uNtp0MDGIiBF0njUoUqld76lNC7WFzYDYBxOzvnE9DemOFxFapQp4NcO73dSuoRU1bkh9VVs1rneMjnx7jHYWnVR6TrrI6lXGYurCxz3ds5bo70HwuCqNWR6j1CCqa5SyKcjYKBdrXF+BOWcC5xU53SgybsM6LEyg0kMjKPpmEfWSm3FVPiAZvkHQzXw+HPGlT/IJOnNsiIgIiICIiAiIgUGnmvUprwVj6xA/xkXG4Ba9Cth2NlqI6E8NZSL9xse6Z6TbWrt9UKvs1v8AKSaE3MZuvzlpLDYzBO+Gql6dicr9Rx6SE5EHiO/OSOi/R6rjqyoit5IMDXqWOqiXu3W3uRkBtJPC5H6IrUkcarorrwdFceBE1uoVdVQFUbAoCgdgGUnDphCNdrbLG3ZumdeirqUbYfYdxmnAnrt9kyTKjlG0S9GqtZUZ9Vw2qtiDY3yO1fbLitpCtWXUCGmp865u3MbB7pZNMAgmf5/V604aiFUAbBskkCFWZTSPLRaNaLnhAw8mt76ovx1RfxnpE9JbhMGc8ICemazVEeUgZGaXmZaYOYFfiZRaQ3y+xMoseNso7vo418Lhv6ajwFvhLOU/RNr4Sh2MPB2HwlxObb2IiAiIgIiICImnE1NVHb0VY+AJgcwG1nqPxdrdl7D2Wk+lK/BLkJZUhl++M2wzy/ZN/HbI9Y27JFRH+Usetq2FvO1dW3h53fJGKbI/vPd7YHujvPb7LSUJF0Z51Q7gh9slCB4RPQJ7MWbdA9LT0LxhFipUVRdjYfHgBvPIQMgIvIT4xj5i2HFs/wAIPx7ppZ2PnVG7jqe1bQLImYmVh+2/9yp/+pktQjZUYdp1/wA94E50Ei1KZGyZLiW+kARxXI+qTn4902BgwuDce48CNx5GBD8qRkZ75S82V6QMrnYqc9kDbXMpceNstWe4lXjthlHXdDj/AKSlyNT/AJHl5Of6FH/TAcHf81/jOgmLrUx7ERIpERAREQPJX6be1F+eqvrMAfYTLCVHSJrU0HF1HgGPwlmpVbhRJyZdnuP7/fCJhxJqzTLF6y+kPEX8JArvfs95/T99s2s+Ur3BJAG0m0CxwCWplt7nL7K/9zaJmwA1VGxQB+swJgYu89RZqTM3m53CKWbYBc8ewczs74GGJxAQDK7HzV2XttJ4AXGfPnK8gk67m7eAA4Abh+mdznPASSaj+e3fYDYo5C/fcneZ6sDCrWA2nsG89gmAdjsXLiTuv+mfskjUF72z4zPUgRWWpc21bZ2vfibezV9sF2Frpfjbdnwz3fvfJFxxHjPYGpGBzU/vmN0yU53vZtx5cCN45e45zMIL3tnsvy/YnrJA2K+tcEWYbR8RykTFUribc+xh5p+B5Hf+oEychhceG8EZEHsII7oFAXKkqZoxTXElaUp5aw2iVj1LiUdh0Gb/AE78qrD8Kn4zpJzHQM/MVeVZv+OmZ08xdamPYiJFIiICIiB5KTpGcqI+uT4Lb4y7lF0kOdHtb/GWalxHw8lrIeHMliaZacQZrwKXcHcLmZ157o8eeeVoEq8wrNYTOR8Qdg5wNtAZSNpB7slPcOu3iQnuY9wkujskKlTL1agBtdioJ3BFCn2hu8wNLZnlNiib8VogqrutQkgXAKgA94lXo7FF1uRY3II5g2Pd+skEjH42nRRqjkAAE5kAADaSeE+Yad6f1GJFKypuZgST2Lu78+UfxJ00zP5EHqrYtzb6I7rX7xOAZrZnzt990dWRfr0rxd7+XfwS35Z02gun9RSFrjXp72UWdeer9Luz5GcHUw1dFV3p1FVhdSVK3XiAcyOdp5Sa+Y2++F5H6GwuJR0SojBkcAqwNwQeclLPmf8ADPS5FQ4Rz83UDNTz2VVGswHaoZu1Dxn0pD++cRl5UXfwmN8+TC/31sD3kW9Qzcwkd9gPosvgTqn8LGUQscmRnM3sWXgZ1OME5bFZVDzEo7PoEfmqw/8AMf8AjSdTOU6A/wC3X/q/4JOrmLrUx7ERIpERAREQPJRdJNtE829yy9lJ0lHVpH65HipPwlmpcRMPJayFhjJizTLTXmzAjqv2iYVhM8D5r9ogbhIuJOYkqRMZuPOBJonKadDkCo1/TrePlG/7nuGaQMQHBqBDZlckXvbrgOfzyUSelmmFp0mVW6xyPZOe6MVtekW+u48LSo0pofGVixNRBwBL/BZfdHtG/J6SU9YsQWLMRa7sbmw3DYB2QPkPTG/yqsD6Y8NRLSloVFWpTZwDTFRS6kXBQMCwPK07v+JehmWoK6jqPZWNtlQbL9oy+7znCmnrX/EOfHskrUx3/SfpRTxKJrBQQCDsuZwuGXNuGt7d/wAJpTDnIazWGwX+NpPpU7WUDPcPiYF70MU/LMGRt8sLdhDBvwlp9o+k3bPnP8N9Ea1Y4lh81h1YK25sQ6lSBx1UZiebLPo1MbztOfjLErZaRa3mVOySjItbzftMo7tYE+wGVEbHnbOTxx+c7vjOnx77ZylU3qNyAlHbdAT83XH/AJB+UfpOsnJdAfMxH21/LOtmLrUx7ERIpERAREQPJT9JV+bQ8Ki+5h8ZcSr6RD5hjwZD+NR8ZZqXFRhjJyGV+FMsEmmWFUTLAbKg5AzyrGBPWYcVMDeJGxaXBkkTCoMoEPCvsmWKWzq+5hqHtFyviC3gJGB1XI3bpOsHUqd+/eCMwR2GxgRVS2U2BZhnvHWXJh8Ry3ibFaBHx2Cp1UanUUMjCxB4T5lpz+HmIRi+H+dp7hrKlReWdlbtBB5T6olRTcA5i9x2bf8A3MrQPhidG8ZrapwuIvyw9T82rb2zqNBdAcS5DV7Yal9K7I9ZhwUC6rfixy9Ez6YC3H3RqE7Tftk4vWnC4WnTRKFFNSinmjPM3uSScyScyTmTJKieMQouTYDfPWYCVGNU5W4yPWPWA3ILn7bCw8F1r/bE2u9hrEXJyVd5bcPjfcATukGu+qLXuTcsdl2O09m4cgIEDSNXbKbB0tYM4zNySOU2aVrMdWmn+5UYU05M17t2KoZvuzp8Bo+miCmiDUUWvvLAZsTtJ5yjZ0D83EfbX8s6ycn0FN/lhHm+WsPuqBOsmLrUx7ERIpERAREQEg6YS9CqOCk+r1vhJ01V6esrr6QI8RaByeDbISxQypwDZCWlMzbDN5hhjZ1m0zQ2RB5wJbDMwZ7U2345zyBX46jcXG0bJpwuJ3HbLOol5T43DEHWXbvHGBZONbMZMNnAjgeXPd4g6LZm2TDap/ft2SHhsbu375ODq1r7RsINiOw/sRwamUE53B7T7u+ZKagG0NmvLL6R7e+bCp3gMO5W8Dke247JgVUfSK/aBA8TlACrU30+3rAz0NUIzspK52OYe+0bbiYkp/8Aavis9Bp+mW+yrN7QMoGSm28s3Pd2cBkPCZMQti+0+aozLHgB8dg3zDyhHmqE5tZm7lBt3k5cDI1SsFubksdrE3Y9+4chYcoGyrUPnNbWtYAZhRwHE8T+zSaQxgF7nKMfpEC+cploPVN28zhx7ZRZ9GMIzscW484FMOp3U79dzwLlR91V4mXXSDG+Qo6qn5x+qnadrfvlImGxpooqCnrqo6udiOUqMc9Sq5q1BbKyLtCr+sg6b+HKWo1v6n+CTr5y3QD/AGa39Y/kpzqZm61MexESKREQEREBERA4krqVKlP0XYDsJuPYRLCk8j9JaOpWWp9FxY/bX9Vt6pmrD15tirUNNbia0qzYriBJGar2RCuLTFngezCogMa09vApsdo+/WXJuI+MrvlTobOMuI2TqGAMiV8KrboFbQ0op3yWmPHGV+J0KpzGR5ZSvfRVUea577GB0Jxw4+2aamkBxnPNgcT6Y8P+54NGVjtc9wAlFnidKqN8qq2kXc2QE890lUdBDaxJ7TeWeH0cq7BApsLo1mOs+Z9gl3RwgUbJLSkBMmEgiVEEqcdvlvXaUekKm2Udb0ES2Hc+lVc+Cov+M6WUfQ2kVwlG+1tZu5nYj2Wl5MXWpj2IiRSIiAiIgIiIEHSeCWtTamcr5q29WGwj95i4nB1Heg5pVBZhs4Mu5lO8T6VIGk9F0q6alVLj6J2Mp4qw2fu8svEs64+ljxxkpMYOMiY/ofiVzo1FqLuDHyb+PmseeUqH0bpBNuFc/Z1H/KTNdjPK6YY7nNqYsHfOSXCaQbJcJVvzXUHixAlro3o1pFjrVGp0l3Ak1G8FNh4x8OL4VxxnvlxKPFaO0hTP+1rr6VN1b8JsfZIz1sWou1B0HF11R4mB0vlhPfKicqmMxTC64asy7itGoynsIFjM/lGM/lK/9ip+kDpS4mDETnvlGM/la/8AZqfpPflGL/la/wDYqfpAvSBPLCUfl8X/ACtf+xU/SPLYv+Vr/wBmp+kC9uI1hKRTjDswtXvpsvvmwUccdmFfv8mPe0C1aoJoqVxIDYHSFifkzevSv4a014fReLq5KoU79csgXkcr35WgZYrFDjKdKb4iqlBM3c5naFT6TnkB8BvnR0uhNZj87iVVd4poWPrNa3gZ02h9CUMMCKSdY+c7HWdrcT8BYcpL6WeU/DUVREpqLKihVH1VFh7puiJloiIgIiICIiAiIgIiICIiAiIgJiwByIymUQEREBERAREQEREBERAREQEREBERAREQP//Z',
        },
      ],
      shoppingCart: []
    }
  },
watch: {
    shoppingCart: {
        handler(newValue) {
            /// Updates the item in local storage

            localStorage.setItem(
                'shoppingCart', JSON.stringify(newValue));

        }, deep: true
    }
},
mounted() {
    /// Retrieves cart from local storage when user first loads

    this.shoppingCart = JSON.parse(
        localStorage.getItem('shoppingCart') || "[]")

},

  methods: {
    addToCart(product) {
      let exists = false
      for (const cartItem of this.shoppingCart) {
        if (cartItem.id === product.id) {
          cartItem.amount = cartItem.amount + 1
          exists = true;
          break;
        }
      }
      if (!exists) {
        this.shoppingCart.push({
          ...product,
          amount: 1,
        })
      }
    },
  },
}
</script>
