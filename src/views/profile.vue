<template>
  <div class="min-h-full">
    <Disclosure as="nav" class="bg-gray-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <img class="h-8 w-8" src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg" alt="Workflow" />
            </div>
            <div class="hidden md:block">
              <div class="ml-10 flex items-baseline space-x-4">
                <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'px-3 py-2 rounded-md text-sm font-medium']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</a>
              </div>
            </div>
          </div>
          <div class="hidden md:block">
            <div class="ml-4 flex items-center md:ml-6">
              <button type="button" class="bg-gray-800 p-1 rounded-full text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
                <span class="sr-only">View notifications</span>
                <!-- <BellIcon class="h-6 w-6" aria-hidden="true" /> -->
              </button>

              <!-- Profile dropdown -->
              <Menu as="div" class="ml-3 relative">
                <div>
                  <MenuButton class="max-w-xs bg-gray-800 rounded-full flex items-center text-sm focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
                    <span class="sr-only">Open user menu</span>
                    <img class="h-8 w-8 rounded-full" :src="user.avatar" alt="" />
                  </MenuButton>
                </div>
                <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                  <MenuItems class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
                    <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                      <a :href="item.href" :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">{{ item.name }}</a>
                    </MenuItem>
                  </MenuItems>
                </transition>
              </Menu>
            </div>
          </div>
          <div class="-mr-2 flex md:hidden">
            <!-- Mobile menu button -->
            <DisclosureButton class="bg-gray-800 inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
              <span class="sr-only">Open main menu</span>
              <!-- <MenuIcon v-if="!open" class="block h-6 w-6" aria-hidden="true" /> -->
              <!-- <XIcon v-else class="block h-6 w-6" aria-hidden="true" /> -->
            </DisclosureButton>
          </div>
        </div>
      </div>

      <DisclosurePanel class="md:hidden">
        <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
          <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href" :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'block px-3 py-2 rounded-md text-base font-medium']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</DisclosureButton>
        </div>
        <div class="pt-4 pb-3 border-t border-gray-700">
          <div class="flex items-center px-5">
            <div class="flex-shrink-0">
              <!-- <img class="h-10 w-10 rounded-full" :src="user.imageUrl" alt="" /> -->
            </div>
            <div class="ml-3">
              <!-- <div class="text-base font-medium leading-none text-white">{{ user.name }}</div>
              <div class="text-sm font-medium leading-none text-gray-400">{{ user.email }}</div> -->
            </div>
            <button type="button" class="ml-auto bg-gray-800 flex-shrink-0 p-1 rounded-full text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
              <span class="sr-only">View notifications</span>
              <!-- <BellIcon class="h-6 w-6" aria-hidden="true" /> -->
            </button>
          </div>
          <div class="mt-3 px-2 space-y-1">
            <DisclosureButton v-for="item in userNavigation" :key="item.name" as="a" :href="item.href" class="block px-3 py-2 rounded-md text-base font-medium text-gray-400 hover:text-white hover:bg-gray-700">{{ item.name }}</DisclosureButton>
          </div>
        </div>
      </DisclosurePanel>
    </Disclosure>

    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold text-gray-900">Профиль</h1>
      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Replace with your content -->
        <div class="px-4 py-6 sm:px-0">
            <div class="grid grid-cols-2">
                <div>
                    <h2 class="text-2xl">
                        Личная информация
                    </h2>
                    <p>
                        <img class="w-40" :src="user.avatar" alt="Аватарка">
                    </p>
                    <div class="flex">
                        <p>Имя: </p>
                        <p v-text="user.first_name"></p>
                    </div>
                    <div class="flex">
                        <p>Фамилия: </p>
                        <p v-text="user.last_name"></p>
                    </div>
                    <div class="flex">
                        <p>Возраст: </p>
                        <p>{{ageCurrent}}</p>
                    </div>
                    <div class="flex">
                        <p>Должность: </p>
                        <p>{{position.title}}</p>
                    </div>
                </div>
                <div>
                    <h2 class="text-2xl mt-2">
                        Рекомендованное пиво 
                    </h2>
                    <div class="flex">
                        <p>Названия: </p>
                        <p v-text="beer.name"></p>
                    </div>
                    <div class="flex">
                        <p>Алкоголь: </p>
                        <p v-text="beer.alcohol"></p>
                    </div>
                    <div class="flex">
                        <p>Корп: </p>
                        <p v-text="beer.blg"></p>
                    </div>
                    <div class="flex">
                        <p>Бренд: </p>
                        <p v-text="beer.brand"></p>
                    </div>
                    <div class="flex">
                        <p>hop: </p>
                        <p v-text="beer.brand"></p>
                    </div>
                    <div class="flex">
                        <p>ibu: </p>
                        <p v-text="beer.ibu"></p>
                    </div>
                    <div class="flex">
                        <p>malts: </p>
                        <p v-text="beer.malts"></p>
                    </div>
                    <div class="flex">
                        <p>Стиль: </p>
                        <p v-text="beer.style"></p>
                    </div>
                    <div class="flex">
                        <p>Год: </p>
                        <p v-text="beer.yeast"></p>
                    </div>
                </div>
            </div>
          
        </div>
        <!-- /End replace -->
      </div>
    </main>
  </div>
</template>

<script>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'

// console.log(this.user.date_of_birth);

    export default {
      components: {
        Disclosure,
        DisclosureButton,
        DisclosurePanel,
        Menu,
        MenuButton,
        MenuItem,
        MenuItems,
      },
      data(){
          return {
              user: {},
              beer: {}
          }
      },
      setup() {
        return {
          navigation,
          userNavigation,
        }
      },
      computed: {
          ageCurrent(){
            const date = new Date();

            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();

            const withHyphens = [year, month, day].join('-');
            
            var date1 = new Date(withHyphens);
            var date2 = new Date(this.user.date_of_birth);
            var timeDiff = Math.abs(date2.getTime() - date1.getTime());
            var diffDays = Math.ceil(timeDiff / (1000 * 3600 * 24));
            let result = diffDays / 364
            return result.toFixed() 
        },
        position(){
            var employment = Object.assign({}, this.user.employment);
            return employment
        }
      },
      mounted(){
        this.axios.get('https://random-data-api.com/api/users/random_user')
            .then(res=>{
                this.user = res.data
            }).catch(err=> {
                console.log(err);
            }),

        this.axios.get('https://random-data-api.com/api/beer/random_beer')
            .then(res=>{
                this.beer = res.data
            }).catch(err=> {
                console.log(err);
            })
      }
    }

// const user = {
//   name: 'Tom Cook',
//   email: 'tom@example.com',
//   imageUrl:
//     'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
// }
const navigation = [
  { name: 'Dashboard', href: '#', current: true },
  { name: 'Team', href: '#', current: false },
  { name: 'Projects', href: '#', current: false },
  { name: 'Calendar', href: '#', current: false },
  { name: 'Reports', href: '#', current: false },
]
const userNavigation = [
  { name: 'Sign out', href: '#' }
]

</script>