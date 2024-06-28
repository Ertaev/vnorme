<template>
    <div class="container">
        <div class="filter" :class="{ opened: filterOpened }">
            <div class="filter__inner">
                <div class="filter__top">
                    <p @click="toggleFilterSidebar"><i class="icon arrow-icon"></i> Назад</p>

                    <div @click="toggleFilterSidebar" class="close"></div>
                </div>

                <div class="filter__content">
                    <div class="filter__box">
                        <p>Что вас беспокоит</p>

                        <div class="filter__inputs">
                            <div
                                v-for="filterItem of filterList"
                                class="filter__checkbox"
                                :key="filterItem"
                                @click="toggleFilter(filterItem.substr(3))"
                                :class="{active: activeFilters.includes(filterItem.substr(3))}"
                            >
                                <svg v-if="!activeFilters.includes(filterItem.substr(3))" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM4.69325 2.44506C4.16715 2.48805 3.8981 2.56596 3.71042 2.66159C3.25884 2.89168 2.89168 3.25884 2.66159 3.71042C2.56596 3.8981 2.48805 4.16715 2.44506 4.69325C2.40093 5.23335 2.4 5.93211 2.4 6.96V17.04C2.4 18.0679 2.40093 18.7666 2.44506 19.3068C2.48805 19.8329 2.56596 20.1019 2.66159 20.2896C2.89168 20.7412 3.25884 21.1083 3.71042 21.3384C3.8981 21.434 4.16715 21.512 4.69325 21.5549C5.23335 21.5991 5.93211 21.6 6.96 21.6H17.04C18.0679 21.6 18.7666 21.5991 19.3068 21.5549C19.8329 21.512 20.1019 21.434 20.2896 21.3384C20.7412 21.1083 21.1083 20.7412 21.3384 20.2896C21.434 20.1019 21.512 19.8329 21.5549 19.3068C21.5991 18.7666 21.6 18.0679 21.6 17.04V6.96C21.6 5.93211 21.5991 5.23335 21.5549 4.69325C21.512 4.16715 21.434 3.8981 21.3384 3.71042C21.1083 3.25884 20.7412 2.89168 20.2896 2.66159C20.1019 2.56596 19.8329 2.48805 19.3068 2.44506C18.7666 2.40093 18.0679 2.4 17.04 2.4H6.96C5.93211 2.4 5.23335 2.40093 4.69325 2.44506Z" fill="#F2F2F2"/>
                                </svg>

                                <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM18.2485 7.55147C18.7172 8.0201 18.7172 8.7799 18.2485 9.24853L11.0485 16.4485C10.5799 16.9172 9.8201 16.9172 9.35147 16.4485L5.75147 12.8485C5.28284 12.3799 5.28284 11.6201 5.75147 11.1515C6.2201 10.6828 6.9799 10.6828 7.44853 11.1515L10.2 13.9029L16.5515 7.55147C17.0201 7.08284 17.7799 7.08284 18.2485 7.55147Z" fill="url(#paint0_linear_36_10540)"/>
                                    <defs>
                                    <linearGradient id="paint0_linear_36_10540" x1="30.5" y1="-6.40275" x2="0.298248" y2="23.5083" gradientUnits="userSpaceOnUse">
                                    <stop offset="0.314617" stop-color="#00FFF0"/>
                                    <stop offset="0.869792" stop-color="#FAFF00"/>
                                    </linearGradient>
                                    </defs>
                                </svg>

                                <span>
                                    {{ filterItem }}
                                </span>
                            </div>
                        </div>
                    </div>

                    <div class="filter__box">
                        <p>Методы психолога</p>

                        <div class="filter__inputs">
                            <div
                                v-for="methodItem of methodList"
                                class="filter__checkbox"
                                :key="methodItem"
                                @click="toggleMethod(methodItem)"
                                :class="{active: activeMethods.includes(methodItem)}"
                            >
                                <svg v-if="!activeMethods.includes(methodItem)" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM4.69325 2.44506C4.16715 2.48805 3.8981 2.56596 3.71042 2.66159C3.25884 2.89168 2.89168 3.25884 2.66159 3.71042C2.56596 3.8981 2.48805 4.16715 2.44506 4.69325C2.40093 5.23335 2.4 5.93211 2.4 6.96V17.04C2.4 18.0679 2.40093 18.7666 2.44506 19.3068C2.48805 19.8329 2.56596 20.1019 2.66159 20.2896C2.89168 20.7412 3.25884 21.1083 3.71042 21.3384C3.8981 21.434 4.16715 21.512 4.69325 21.5549C5.23335 21.5991 5.93211 21.6 6.96 21.6H17.04C18.0679 21.6 18.7666 21.5991 19.3068 21.5549C19.8329 21.512 20.1019 21.434 20.2896 21.3384C20.7412 21.1083 21.1083 20.7412 21.3384 20.2896C21.434 20.1019 21.512 19.8329 21.5549 19.3068C21.5991 18.7666 21.6 18.0679 21.6 17.04V6.96C21.6 5.93211 21.5991 5.23335 21.5549 4.69325C21.512 4.16715 21.434 3.8981 21.3384 3.71042C21.1083 3.25884 20.7412 2.89168 20.2896 2.66159C20.1019 2.56596 19.8329 2.48805 19.3068 2.44506C18.7666 2.40093 18.0679 2.4 17.04 2.4H6.96C5.93211 2.4 5.23335 2.40093 4.69325 2.44506Z" fill="#F2F2F2"/>
                                </svg>

                                <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM18.2485 7.55147C18.7172 8.0201 18.7172 8.7799 18.2485 9.24853L11.0485 16.4485C10.5799 16.9172 9.8201 16.9172 9.35147 16.4485L5.75147 12.8485C5.28284 12.3799 5.28284 11.6201 5.75147 11.1515C6.2201 10.6828 6.9799 10.6828 7.44853 11.1515L10.2 13.9029L16.5515 7.55147C17.0201 7.08284 17.7799 7.08284 18.2485 7.55147Z" fill="url(#paint0_linear_36_10540)"/>
                                    <defs>
                                    <linearGradient id="paint0_linear_36_10540" x1="30.5" y1="-6.40275" x2="0.298248" y2="23.5083" gradientUnits="userSpaceOnUse">
                                    <stop offset="0.314617" stop-color="#00FFF0"/>
                                    <stop offset="0.869792" stop-color="#FAFF00"/>
                                    </linearGradient>
                                    </defs>
                                </svg>

                                <span>
                                    {{ methodItem }}
                                </span>
                            </div>
                        </div>
                    </div>

                    <div class="filter__box">
                        <p>Возрастная группа</p>

                        <div class="filter__inputs">
                            <div
                                v-for="ageGroup of ageGroups"
                                class="filter__checkbox"
                                :key="ageGroup"
                                @click="toggleAgeGroup(ageGroup)"
                                :class="{active: activeAgeGroups.includes(ageGroup)}"
                            >
                                <svg v-if="!activeAgeGroups.includes(ageGroup)" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM4.69325 2.44506C4.16715 2.48805 3.8981 2.56596 3.71042 2.66159C3.25884 2.89168 2.89168 3.25884 2.66159 3.71042C2.56596 3.8981 2.48805 4.16715 2.44506 4.69325C2.40093 5.23335 2.4 5.93211 2.4 6.96V17.04C2.4 18.0679 2.40093 18.7666 2.44506 19.3068C2.48805 19.8329 2.56596 20.1019 2.66159 20.2896C2.89168 20.7412 3.25884 21.1083 3.71042 21.3384C3.8981 21.434 4.16715 21.512 4.69325 21.5549C5.23335 21.5991 5.93211 21.6 6.96 21.6H17.04C18.0679 21.6 18.7666 21.5991 19.3068 21.5549C19.8329 21.512 20.1019 21.434 20.2896 21.3384C20.7412 21.1083 21.1083 20.7412 21.3384 20.2896C21.434 20.1019 21.512 19.8329 21.5549 19.3068C21.5991 18.7666 21.6 18.0679 21.6 17.04V6.96C21.6 5.93211 21.5991 5.23335 21.5549 4.69325C21.512 4.16715 21.434 3.8981 21.3384 3.71042C21.1083 3.25884 20.7412 2.89168 20.2896 2.66159C20.1019 2.56596 19.8329 2.48805 19.3068 2.44506C18.7666 2.40093 18.0679 2.4 17.04 2.4H6.96C5.93211 2.4 5.23335 2.40093 4.69325 2.44506Z" fill="#F2F2F2"/>
                                </svg>

                                <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path fill-rule="evenodd" clip-rule="evenodd" d="M6.91044 5.17549e-07H17.0896C18.0555 -1.47889e-05 18.8528 -2.73764e-05 19.5022 0.0530334C20.1767 0.108144 20.7968 0.226421 21.3792 0.52317C22.2823 0.983362 23.0166 1.71767 23.4768 2.62085C23.7736 3.20325 23.8919 3.82329 23.947 4.49781C24 5.14724 24 5.94446 24 6.91041V17.0896C24 18.0555 24 18.8528 23.947 19.5022C23.8919 20.1767 23.7736 20.7968 23.4768 21.3792C23.0166 22.2823 22.2823 23.0166 21.3792 23.4768C20.7968 23.7736 20.1767 23.8919 19.5022 23.947C18.8528 24 18.0555 24 17.0896 24H6.91041C5.94446 24 5.14724 24 4.49781 23.947C3.82329 23.8919 3.20325 23.7736 2.62085 23.4768C1.71767 23.0166 0.983362 22.2823 0.52317 21.3792C0.226421 20.7968 0.108144 20.1767 0.0530334 19.5022C-2.73764e-05 18.8528 -1.47889e-05 18.0555 5.17552e-07 17.0896V6.91044C-1.47889e-05 5.94448 -2.73764e-05 5.14724 0.0530334 4.49781C0.108144 3.82329 0.226421 3.20325 0.52317 2.62085C0.983362 1.71767 1.71767 0.983362 2.62085 0.52317C3.20325 0.226421 3.82329 0.108144 4.49781 0.0530334C5.14724 -2.73764e-05 5.94448 -1.47889e-05 6.91044 5.17549e-07ZM18.2485 7.55147C18.7172 8.0201 18.7172 8.7799 18.2485 9.24853L11.0485 16.4485C10.5799 16.9172 9.8201 16.9172 9.35147 16.4485L5.75147 12.8485C5.28284 12.3799 5.28284 11.6201 5.75147 11.1515C6.2201 10.6828 6.9799 10.6828 7.44853 11.1515L10.2 13.9029L16.5515 7.55147C17.0201 7.08284 17.7799 7.08284 18.2485 7.55147Z" fill="url(#paint0_linear_36_10540)"/>
                                    <defs>
                                    <linearGradient id="paint0_linear_36_10540" x1="30.5" y1="-6.40275" x2="0.298248" y2="23.5083" gradientUnits="userSpaceOnUse">
                                    <stop offset="0.314617" stop-color="#00FFF0"/>
                                    <stop offset="0.869792" stop-color="#FAFF00"/>
                                    </linearGradient>
                                    </defs>
                                </svg>

                                <span>
                                    {{ ageGroup }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="filter__bottom">
                    <p>
                        Нашлось психологов:
                        {{ filteredPsychologists.length }}
                    </p>

                    <div class="buttons">
                        <div
                            @click="applyFilters"
                            class="button button--gradient"
                        >
                            Применить
                        </div>
                        <div
                            @click="resetFilters"
                            class="button button--grey"
                        >
                            Сбросить фильтры
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="main__title">
            <h1 class="title">Выберите подходящего психолога</h1>

            <p class="text">{{ filteredPsychologists.length }} психологов</p>
        </div>

        <div class="search-block">
            <form>
                <div class="search-block__input">
                    <input
                        type="text"
                        v-model="searchQuery"
                        placeholder="Найти специалиста"
                    />
                </div>

                <button class="button button--gradient">Найти</button>
            </form>
        </div>

        <div class="filter__list">
            <div
                v-for="filterItem of filterList"
                class="filter__item"
                :key="filterItem"
                @click="toggleFilter(filterItem.substr(3))"
                :class="{
                    active: activeFilters.includes(filterItem.substr(3)),
                }"
            >
                {{ filterItem }}
            </div>

            <div class="filter__item" @click="resetFilters">
                Сбросить фильтры
            </div>
        </div>

        <div class="mobile-filter">
            <div @click="toggleFilterSidebar" class="mobile-filter__item">
                <i class="icon filter-icon"></i>
                Все фильтры
                <span>{{
                    activeFilters.length +
                    activeMethods.length +
                    activeAgeGroups.length
                }}</span>
            </div>

            <div
                @click="toggleShowFavorites"
                class="mobile-filter__item __favorites"
            >
                Только избранные
                <i class="icon like-icon"></i>
            </div>

            <div class="mobile-filter__item" @click="resetFilters">
                Сбросить фильтры
            </div>
        </div>

        <div class="psychologists">
            <div
                v-for="psychologist of filteredPsychologists"
                class="psychologist"
                :key="psychologist.id"
            >
                <div class="psychologist__left">
                    <div class="psychologist__img">
                        <img
                            :src="psychologist.image"
                            :alt="psychologist.name"
                        />

                        <div class="sticker">
                            Онлайн сессия {{ psychologist.price }} ₽
                        </div>
                    </div>

                    <div class="psychologist__buttons">
                        <div class="button button--gradient">
                            <i class="icon clock-icon"></i>
                            Записаться
                        </div>
                        <div class="button button--grey">
                            Подробнее о психологе
                        </div>
                    </div>
                </div>

                <div class="psychologist__content">
                    <div class="psychologist__title">
                        <h4>
                            {{ psychologist.name }}
                        </h4>

                        <div class="psychologist__text">
                            <p>Опыт {{ psychologist.experience }}</p>
                            <p>Возраст {{ psychologist.age }}</p>
                        </div>
                    </div>

                    <div class="psychologist__methods">
                        <p>Методики:</p>

                        <div class="methods__list">
                            <div
                                v-for="method of psychologist.methods"
                                class="methods__item"
                            >
                                {{ method }}
                                <i class="icon info-icon"></i>
                            </div>
                        </div>
                    </div>

                    <div class="psychologist__queries">
                        <p>Работает с запросами:</p>

                        <ul class="query__list">
                            <li
                                v-for="query of psychologist.queries"
                                class="query__item"
                            >
                                {{ query }}
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <div class="psychologist psychologist--blur">
                <p>
                    Зарегистрируйтесь и получите доступ ко полному списку
                    специалистам
                </p>

                <div class="buttons">
                    <RouterLink to="/" class="button button--grey">
                        Зарегистрироваться
                    </RouterLink>

                    <RouterLink to="/" class="button button--white">
                        Войти
                    </RouterLink>
                </div>
            </div>
        </div>

        <div class="psychologists-mobile">
            <div
                v-for="psychologist of filteredPsychologists"
                class="psychologist"
                :key="psychologist.id"
            >
                <div class="psychologist__head">
                    <div class="psychologist__title">
                        <h4>
                            {{ psychologist.name }}
                        </h4>

                        <div class="psychologist__text">
                            <p>Опыт {{ psychologist.experience }}</p>
                            <p>Возраст {{ psychologist.age }}</p>
                        </div>
                    </div>

                    <div>
                        <i
                            @click="toggleFavorite(psychologist)"
                            class="icon like-icon"
                        ></i>
                    </div>
                </div>

                <div class="psychologist__desc">
                    <div class="psychologist__img">
                        <img
                            :src="psychologist.image"
                            :alt="psychologist.name"
                        />

                        <div class="sticker">
                            Онлайн сессия {{ psychologist.price }} ₽
                        </div>
                    </div>

                    <div class="psychologist__methods">
                        <p>Методы:</p>

                        <div class="methods__list">
                            <div
                                v-for="method of psychologist.methods"
                                class="methods__item"
                            >
                                {{ method }}
                                <i class="icon info-icon"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="psychologist__queries">
                    <p>Работает с запросами:</p>

                    <ul class="query__list">
                        <li
                            v-for="query of psychologist.queries"
                            class="query__item"
                        >
                            {{ query }}
                        </li>
                    </ul>
                </div>

                <div class="psychologist__buttons">
                    <div class="button button--gradient">
                        <i class="icon clock-icon"></i>
                        Записаться
                    </div>
                    <div class="button button--grey">Подробнее о психологе</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from "vue";

const filterOpened = ref(false);
const searchQuery = ref("");
const activeFilters = ref([]);
const activeMethods = ref([]);
const activeAgeGroups = ref([]);
const showFavorites = ref(false);
const isFilterSidebarVisible = ref(false);

const toggleFilterSidebar = () => {
    filterOpened.value = !filterOpened.value;

    document.documentElement.style.overflow = filterOpened.value ? "hidden" : "auto"
};

const filterList = ref([
    "😴 Проблемы со сном",
    "💑 Отношения с партнёром",
    "🌯 Пищевое поведение",
    "🔎 Поиск себя",
    "😞 Упадок сил",
    "😨 Панические атаки",
    "😔 Чувство одиночества",
    "🤯 Непонятные эмоции",
]);

const methodList = ref([
    "Гештальт-терапия",
    "Арт-терапия",
    "Принятие и ответственности (АСТ) / Сфокусирование на сострадании (CFT)",
    "Психодинамические подходы",
    "КПТ/КБТ: Когнитивно-поведенческая терапия",
    "Клиническая психология",
]);

const ageGroups = [
    "от 8 до 12 лет",
    "от 12 до 16 лет",
    "от 16 до 20 лет",
    "от 25 до 45 лет",
];

const psychologists = ref([
    {
        id: 1,
        name: "Татьяна Сачкова",
        experience: "9 лет",
        age: "30 лет",
        methods: ["Клиническая психология"],
        queries: [
            "Проблемы со сном",
            "Поиск себя",
            "Упадок сил ",
            "Панические атаки",
            "Чувство одиночества",
            "Утрата",
            "Пищевое поведение",
        ],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 2,
        name: "Елена",
        experience: "12 лет",
        age: "30 лет",
        methods: ["Клиническая психология"],
        queries: [
            "Проблемы со сном",
            "Панические атаки",
            "Чувство одиночества",
            "Непонятные эмоции",
            "Тревога и страхи",
            "Утрата",
            "Пищевое поведение",
        ],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 3,
        name: "Татьяна",
        experience: "3 года",
        age: "31 год",
        methods: [
            "Психодинамические подходы",
            "Принятие и ответственности (АСТ) / Сфокусирование на сострадании (CFT)",
            "Клиническая психология",
            "КПТ/КБТ: Когнитивно-поведенческая терапия",
        ],
        queries: ["Непонятные эмоции", "Пищевое поведение"],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 4,
        name: "Сачкова",
        experience: "9 лет",
        age: "30 лет",
        methods: ["Клиническая психология"],
        queries: ["Проблемы со сном", "Поиск себя", "Упадок сил "],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 5,
        name: "Елена Сачкова",
        experience: "12 лет",
        age: "30 лет",
        methods: ["Клиническая психология"],
        queries: ["Непонятные эмоции"],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 6,
        name: "Яна Сачкова",
        experience: "3 года",
        age: "31 год",
        methods: [
            "Психодинамические подходы",
            "Принятие и ответственности (АСТ) / Сфокусирование на сострадании (CFT)",
        ],
        queries: [
            "Проблемы со сном",
            "Панические атаки",
            "Тревога и страхи",
            "Поиск себя",
            "Чувство одиночества",
        ],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
    {
        id: 7,
        name: "Наталья Сачкова",
        experience: "3 года",
        age: "31 год",
        methods: [
            "Психодинамические подходы",
            "Клиническая психология",
            "КПТ/КБТ: Когнитивно-поведенческая терапия",
        ],
        queries: ["Проблемы со сном", "Упадок сил", "Пищевое поведение"],
        price: 3800,
        isFavorite: false,
        image: "src/assets/img/psychologist-1.jpg",
    },
]);

const filteredPsychologists = computed(() => {
    return psychologists.value.filter((psychologist) => {
        const matchesSearch = psychologist.name
            .toLowerCase()
            .includes(searchQuery.value.toLowerCase());
        const matchesFilters =
            activeFilters.value.length === 0 ||
            activeFilters.value.every((filter) =>
                psychologist.queries.includes(filter)
            );
        const matchesMethods =
            activeMethods.value.length === 0 ||
            activeMethods.value.every((method) =>
                psychologist.methods.includes(method)
            );
        const matchesAgeGroups = activeAgeGroups.value.length === 0;
        const matchesFavorites =
            !showFavorites.value || psychologist.isFavorite;
        return (
            matchesSearch &&
            matchesFilters &&
            matchesMethods &&
            matchesAgeGroups &&
            matchesFavorites
        );
    });
});

const toggleFilter = (filter) => {
    if (activeFilters.value.includes(filter)) {
        activeFilters.value = activeFilters.value.filter((f) => f !== filter);
    } else {
        activeFilters.value.push(filter);
    }
};

const toggleMethod = (method) => {
    if (activeMethods.value.includes(method)) {
        activeMethods.value = activeMethods.value.filter((m) => m !== method);
    } else {
        activeMethods.value.push(method);
    }
};

const toggleAgeGroup = (ageGroup) => {
    if (activeAgeGroups.value.includes(ageGroup)) {
        activeAgeGroups.value = activeAgeGroups.value.filter(
            (a) => a !== ageGroup
        );
    } else {
        activeAgeGroups.value.push(ageGroup);
    }
};

const toggleFavorite = (psychologist) => {
    psychologist.isFavorite = !psychologist.isFavorite;
};

const toggleShowFavorites = () => {
    showFavorites.value = !showFavorites.value;
};

const resetFilters = () => {
    activeFilters.value = [];
    activeMethods.value = [];
    activeAgeGroups.value = [];
    showFavorites.value = false;
};

const applyFilters = () => {
    isFilterSidebarVisible.value = false;
};
</script>

<style scoped>
.main__title {
    padding: 40px 0 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.title {
    font-weight: 700;
    font-size: 32px;
    line-height: 48px;

    color: #030303;
}

.text {
    font-weight: 700;
    font-size: 24px;
    line-height: 36px;

    color: #999999;
}

.search-block {
    margin-bottom: 20px;
}

.search-block form {
    display: flex;
    align-items: center;
    gap: 12px;
}

.search-block__input {
    position: relative;
    display: flex;
    width: 100%;
}

.search-block__input::before {
    content: "";
    position: absolute;

    left: 18px;
    top: 50%;
    transform: translateY(-50%);

    width: 24px;
    height: 24px;
    color: #818181;

    background: url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11.5 21C16.7467 21 21 16.7467 21 11.5C21 6.25329 16.7467 2 11.5 2C6.25329 2 2 6.25329 2 11.5C2 16.7467 6.25329 21 11.5 21Z' stroke='%23818181' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3Cpath d='M22 22L20 20' stroke='%23818181' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E%0A");
}

.search-block__input input {
    width: 100%;
    height: 48px;

    padding: 4px 16px 4px 52px;

    background: #ffffff;
    border: 2px solid #dcffea;
    border-radius: 40px;

    font-weight: 400;
    font-size: 16px;
    line-height: 24px;

    color: #1d1b20;
}

.search-block__input input::placeholder {
    font-weight: 400;
    font-size: 16px;
    line-height: 24px;

    color: #818181;
}

.search-block .button {
    width: 90px;
}

.filter__list {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 12px;
    margin-bottom: 40px;
}

.filter__item {
    padding: 8px 12px 8px 8px;
    gap: 10px;
    height: 37px;

    background: #ffffff;
    border-radius: 12px;

    font-weight: 700;
    font-size: 14px;
    line-height: 21px;

    color: #818181;
    cursor: pointer;

    transition: all 0.3s ease;
}

.filter__item:hover {
    background: #dcffea;
}

.filter__item.active,
.filter__item:active {
    background: #c2f2d5;
}

.filter__item:last-child {
    padding: 8px 12px;
    height: 40px;

    background: #c2f2d5;

    font-family: "Inter";
    font-weight: 400;
    font-size: 14px;
    line-height: 21px;

    color: #1d1b20;
    transition: all 0.3s ease;
}

.filter__item:last-child:hover {
    background: #00fff0;
}

.filter__item:last-child:active {
    background: #00e6d8;
}

.psychologists {
    display: flex;
    flex-direction: column;
    gap: 20px;

    margin-bottom: 40px;
}

.psychologist {
    background: #fff;
    padding: 20px 20px 24px;

    display: flex;
    align-items: flex-start;
    gap: 40px;

    width: 100%;

    background: #ffffff;
    border-radius: 32px;
}

.psychologist__img {
    position: relative;
    width: 240px;
    height: 240px;

    border-radius: 20px;
    overflow: hidden;

    margin-bottom: 16px;
}

.psychologist__img img {
    width: 100%;
    height: 100%;
}

.sticker {
    position: absolute;
    left: 8px;
    bottom: 8px;

    padding: 4px 12px;
    width: 205px;
    height: 32px;

    background: #dcffea;
    border-radius: 40px;

    font-weight: 700;
    font-size: 16px;
    line-height: 24px;

    color: #0c9733;
}

.psychologist__buttons {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.psychologist__buttons .button--gradient {
    gap: 8px;
}

.psychologist__content {
    width: 100%;
}

.psychologist__title {
    padding: 4px 0 17px;
    display: flex;
    flex-direction: column;
    gap: 12px;

    border-bottom: 1px solid #f2f2f2;
    margin-bottom: 16px;
}

.psychologist__title h4 {
    font-weight: 700;
    font-size: 24px;
    line-height: 24px;

    color: #030303;
}

.psychologist__text {
    display: flex;
    align-items: center;
    gap: 28px;
}

.psychologist__text p {
    position: relative;

    font-weight: 700;
    font-size: 16px;
    line-height: 24px;

    color: #818181;
}

.psychologist__text p:not(:first-child)::before {
    content: "";
    position: absolute;

    width: 4px;
    height: 4px;

    left: -16px;
    top: 50%;
    transform: translateY(-50%);

    background: url("data:image/svg+xml,%3Csvg width='4' height='4' viewBox='0 0 4 4' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle opacity='0.94' cx='2' cy='2' r='2' fill='%23818181'/%3E%3C/svg%3E%0A");
}

.psychologist__methods {
    margin-bottom: 24px;
}

.psychologist__methods p {
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;

    color: #262626;

    margin-bottom: 16px;
}

.methods__list {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 12px;
}

.methods__item {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5.5px 12px;
    gap: 8px;

    background: #f2f2f2;
    border-radius: 40px;

    font-weight: 700;
    font-size: 14px;
    line-height: 21px;

    color: #818181;
}

.psychologist__queries p {
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;

    color: #262626;
    margin-bottom: 12px;
}

.query__list {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 12px 20px;
}

.query__item {
    position: relative;
    width: calc(100% / 3 - 14px);

    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    padding-left: 14px;

    color: #818181;
}

.query__item::before {
    content: "";
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);

    width: 6px;
    height: 6px;

    background: url("data:image/svg+xml,%3Csvg width='6' height='6' viewBox='0 0 6 6' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle opacity='0.94' cx='3' cy='3' r='3' fill='%23818181'/%3E%3C/svg%3E%0A");
}

.psychologist--blur {
    position: relative;
    background: center / cover no-repeat url(@/assets/img/card.png);
    height: 408px;

    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    gap: 0;
    overflow: hidden;
    z-index: 0;
}

.psychologist--blur::before {
    content: "";
    position: absolute;

    left: 0;
    top: 0;

    width: 100%;
    height: 100%;

    background: linear-gradient(225.28deg, #00fff0 12.52%, #faff00 82.05%);
    opacity: 0.6;

    z-index: -1;
}

.psychologist--blur p {
    max-width: 730px;

    font-weight: 700;
    font-size: 32px;
    line-height: 48px;

    text-align: center;

    color: #030303;

    margin: 0 auto 72px;
}

.psychologist--blur .buttons {
    display: flex;
    align-items: center;
    gap: 35px;
}

.psychologist--blur .button {
    width: 240px;
}

.psychologists-mobile {
    display: none;
}

.mobile-filter {
    display: none;
    flex-wrap: wrap;
    gap: 12px;

    margin-bottom: 40px;
}

.mobile-filter__item {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 8px;
    gap: 4px;
    height: 40px;

    background: #ffffff;
    border-radius: 12px;

    font-family: "Inter";
    font-weight: 400;
    font-size: 14px;
    line-height: 21px;

    color: #818181;
}

.mobile-filter__item span {
    display: flex;
    align-items: center;
    padding: 0px 4px;

    width: 16px;
    height: 18px;

    background: #ff312c;
    border-radius: 12px;

    font-family: "Inter";
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 18px;

    text-align: center;

    color: #ffffff;
}

.mobile-filter__item .like-icon {
    color: #818181;
}

.mobile-filter__item:last-child {
    padding: 8px 12px;
    height: 40px;

    background: #c2f2d5;

    font-family: "Inter";
    font-weight: 400;
    font-size: 14px;
    line-height: 21px;

    color: #1d1b20;
    transition: all 0.3s ease;
}

.mobile-filter__item:last-child:hover {
    background: #00fff0;
}

.mobile-filter__item:last-child:active {
    background: #00e6d8;
}

.filter {
    display: none;
}

@media screen and (max-width: 992px) {
    .main__title {
        padding: 20px 0;
        flex-direction: column;
        align-items: flex-start;
    }

    .title {
        font-size: 24px;
        line-height: 36px;
    }

    .text {
        font-size: 16px;
        line-height: 24px;
    }

    .psychologists {
        display: none;
    }

    .psychologists-mobile {
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    .psychologist {
        padding: 16px 16px 20px;
        border-radius: 20px;
        flex-direction: column;
        gap: 24px;
    }

    .psychologist__head {
        width: 100%;
        display: flex;
        justify-content: space-between;
    }

    .psychologist__title {
        border-bottom: none;
        padding-bottom: 0;
        margin-bottom: 0;
    }

    .psychologist__img {
        min-width: 310px;
        height: 310px;
        margin-bottom: 0;
    }

    .psychologist__desc {
        display: flex;
        gap: 24px;
    }

    .psychologist__methods {
        margin-bottom: 0;
    }

    .methods__item {
        border-radius: 20px;
    }

    .psychologist__queries {
        width: 100%;
        padding-top: 8px;
    }

    .psychologist__buttons {
        flex-direction: row;
        width: 100%;
    }

    .psychologist__buttons .button {
        width: 50%;
    }

    .filter__list {
        display: none;
    }

    .mobile-filter {
        display: flex;
    }

    .mobile-filter__item {
        cursor: pointer;
        transition: all 0.3s ease;
    }

    .mobile-filter__item:hover {
        background: #00fff0;

        color: #1d1b20;
    }

    .mobile-filter__item:hover .icon {
        color: #1d1b20;
    }

    .mobile-filter__item:active {
        background: #00e6d8;
    }

    .filter {
        position: fixed;
        left: 0;
        top: -100vh;

        width: 100%;
        height: 100vh;

        display: block;

        background: #fff;
        padding: 14px 16px 20px;

        overflow-y: scroll;
        z-index: 100;
        transition: all 0.3s ease;
    }

    .filter.opened {
        top: 0;
    }

    .filter__top {
        display: flex;
        align-items: center;
        justify-content: space-between;

        padding-bottom: 20px;
        margin-bottom: 12px;

        border-bottom: 2px solid #dcffea;
    }

    .filter__top p {
        display: flex;
        align-items: center;
        gap: 16px;

        font-family: 'Inter';
        font-weight: 600;
        font-size: 14px;
        line-height: 21px;

        color: #818181;
    }

    .filter__content {
        margin-bottom: 40px;
    }

    .filter__box {
        padding-bottom: 12px;
        margin-bottom: 12px;

        border-bottom: 2px solid #dcffea;
    }

    .filter__box p {
        font-family: "Inter";
        font-weight: 800;
        font-size: 16px;
        line-height: 24px;

        color: #393c41;
        margin-bottom: 8px;
    }

    .filter__inputs {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        gap: 8px;
    }

    .filter__checkbox {
        display: flex;
        padding: 8px 12px 8px 8px;
        gap: 10px;

        border: 1px solid #c6e6d3;
        border-radius: 12px;
        cursor: pointer;
    }

    .filter__checkbox.active {
        background: #dcffea;
    }

    .filter__bottom p {
        font-weight: 400;
        font-size: 14px;
        line-height: 21px;

        text-align: center;

        color: #74767A;

        margin-bottom: 8px;
    }

    .filter__bottom .buttons {
        display: flex;
        flex-direction: column;

        gap: 8px;
    }
}

@media screen and (max-width: 640px) {
    .query__item {
        width: calc(100% / 2 - 10px);
    }

    .psychologist__desc {
        width: 100%;
        flex-direction: column;
    }

    .psychologist__buttons {
        flex-direction: column;
    }

    .psychologist__buttons .button {
        width: 100%;
    }

    .mobile-filter__item:last-child {
        display: none;
    }
}

@media screen and (max-width: 560px) {
    .query__item {
        width: 100%;
    }
}

@media screen and (max-width: 400px) {
    .psychologist__img {
        width: 100%;
        min-width: inherit;
    }

    .psychologist__img img {
        object-fit: cover;
    }
}

@media screen and (max-width: 340px) {
    .psychologist__text {
        gap: 20px;
    }

    .psychologist__text p:not(:first-child)::before {
        left: -12px;
    }

    .psychologist__text p {
        font-size: 14px;
        line-height: 20px;
    }

    .psychologist__img {
        height: 250px;
    }
}
</style>
