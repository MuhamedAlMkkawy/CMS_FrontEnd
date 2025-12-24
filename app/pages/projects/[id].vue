<template>
  <div class="project_page page">
    <div class="side_bar">
      <div class="header_image">
        <button class="back_btn" @click="$router.back()">
          <i class="pi pi-angle-left"></i>
        </button>
        <div class="image">
          <img src="@/assets/images/logo.png" alt="logo_image" loading="lazy" />
        </div>
      </div>
      <hr />
      <ul class="components">
        <div
          v-for="item in sidebarComponents"
          :key="item.type"
          class="component_item"
          draggable="true"
          @dragstart="onDragStart(item)"
        >
          <i :class="item.icon" class="component_icon" />
          <span class="component_title">{{ item.label }}</span>
          <i class="pi pi-equals"></i>
        </div>
      </ul>
    </div>
    <div class="project_content">
      <div class="pages">
        <div
          v-for="i in 8"
          :key="i"
          :class="['page_item', { active: activePage === i }]"
          @click="activePage = i"
        >
          <span>Home</span>
          <Button
            type="button"
            icon="pi pi-ellipsis-v"
            @click.stop="(event) => menu[i - 1].toggle(event)"
            aria-haspopup="true"
            :aria-controls="`overlay_menu_${i}`"
          />
          <Menu
            ref="menu"
            :id="`overlay_menu_${i}`"
            :model="items"
            :popup="true"
          />
        </div>
        <button class="add_page">
          <i class="pi pi-plus"></i>
        </button>
      </div>
    </div>
    <hr />
    <div class="project_sections">
      <div
        v-for="section in sections"
        :key="section.id"
        class="section"
      >
        <div class="section_header">
          <h3 class="section_title">{{ section.name }}</h3>
          <div class="buttons">
            <!-- layout design button -->
            <button
              class="layout_design section_control"
              @click="changeLayout(section)"
            >
              <i
                class="pi pi-stop"
                v-for="i in (section.layout_items === 3 ? 1 : section.layout_items === 1 ? 2 : 3)"
                :key="i"
              ></i>
            </button>

            <button class="section_control pi pi-pen-to-square"></button>
            <button class="section_control pi pi-eye"></button>
          </div>
        </div>

        <hr />
        <div :class="['content_items', `items_${section.layout_items}`]">
          <div
            class="content_item section_component"
            :class="{ 'drag-over': section.isDragOver }"
            @dragover.prevent
            @dragenter="onDragEnter(section)"
            @dragleave="onDragLeave(section)"
            @drop="onDrop(section)"
          >
            <div
              v-for="(comp, index) in section.components"
              :key="comp.id"
              class="section_block"
            >
              <i :class="comp.icon"></i>
              <span>{{ comp.label }}</span>

              <!-- controls -->
              <button class="remove_component" @click.stop="removeComponent(section, index)">
                <i class="pi pi-trash"></i>
              </button>
            </div>

            <!-- empty state -->
            <div v-if="!section.components.length" class="empty_placeholder">
              Drag components here
            </div>
          </div>


        </div>
      </div>

      <div class="section add_section" @click="showAddSectionPopup = true"><i class="pi pi-plus"></i></div>
    </div>
    <AddSectionPopup
      v-if="showAddSectionPopup"
      @handleShowAddSectionPopup="showAddSectionPopup = false"
    />
  </div>
</template>

<script setup>
// ----------------------------
// HANDLE PAGE ITEM 'S MENU
// ----------------------------
const activePage = ref(1);

// -----------------------------
// HANDLE SIDE BAR 'S COMPONENTS
// -----------------------------
const sidebarComponents = [
  {
    type: "card-slider",
    label: "Card slider",
    icon: "pi pi-sliders-h",
  },
  {
    type: "nav-menu",
    label: "Nav menu",
    icon: "pi pi-bars",
  },
  {
    type: "alert",
    label: "Alert",
    icon: "pi pi-exclamation-triangle",
  },
  {
    type: "description-list",
    label: "Description list",
    icon: "pi pi-list",
  },
  {
    type: "divider",
    label: "Divider",
    icon: "pi pi-minus",
  },
  {
    type: "call-to-action",
    label: "Call to action",
    icon: "pi pi-phone",
  },
  {
    type: "card",
    label: "Card",
    icon: "pi pi-id-card",
  },
  {
    type: "pricing-list",
    label: "Pricing list",
    icon: "pi pi-tags",
  },
  {
    type: "data-tables",
    label: "Data tables",
    icon: "pi pi-table",
  },
  {
    type: "buttons",
    label: "Buttons",
    icon: "pi pi-clone",
  },
  {
    type: "modal-module",
    label: "Modal module",
    icon: "pi pi-window-maximize",
  },
  {
    type: "gallery",
    label: "Gallery",
    icon: "pi pi-images",
  },
  {
    type: "timeline",
    label: "Time line",
    icon: "pi pi-clock",
  },
  {
    type: "social-media",
    label: "Social media",
    icon: "pi pi-share-alt",
  },
  {
    type: "custom-html",
    label: "custom HTML",
    icon: "pi pi-code",
  },
  {
    type: "heading",
    label: "Heading",
    icon: "pi pi-heading",
  },
  {
    type: "accordion",
    label: "Accordion",
    icon: "pi pi-align-justify",
  },
  {
    type: "contact-info",
    label: "Contact Info",
    icon: "pi pi-envelope",
  },
  {
    type: "tabs",
    label: "Tabs",
    icon: "pi pi-folder-open",
  },
  {
    type: "logo",
    label: "Logo",
    icon: "pi pi-star",
  },
  {
    type: "back-to-top",
    label: "Back to top",
    icon: "pi pi-arrow-up",
  },
];

// ----------------------------
// HANDLE PAGE ITEM 'S MENU
// ----------------------------
const menu = ref();
const items = ref([
  {
    label: "Options",
        items: [
      {
        label: "Hide",
        icon: "pi pi-eye",
        command: () => {
          router.push("/introduction");
        },
      },
      {
        label: "Delete",
        icon: "pi pi-trash",
        command: () => {
          router.push("/introduction");
        },
      },
      {
        label: "Edit",
        icon: "pi pi-pen-to-square",
        command: () => {
          router.push("/introduction");
        },
      },
    ],
  },
]);


// ----------------------------
// HANDLE SECTION DESIGN
// ----------------------------
const sections = ref([
  {
    id: 1,
    name: "Header",
    layout_items: 3,
    components: [], // { type, label, icon }
    isDragOver: false,
  },
]);


// ------------------------------
// HANDLE DRAG & DROP COMPONENTS
// ------------------------------
const draggedComponent = ref(null);

const onDragStart = (item) => {
  draggedComponent.value = item;
};


const onDragEnter = (section) => {
  section.isDragOver = true;
};

const onDragLeave = (section) => {
  section.isDragOver = false;
};


const onDrop = (section) => {
  if (!draggedComponent.value) return;

  section.components.push({
    id: Date.now(),
    type: draggedComponent.value.type,
    label: draggedComponent.value.label,
    icon: draggedComponent.value.icon,
  });

  section.isDragOver = false;
  draggedComponent.value = null;
};

// ---------------------------
// HANDLE REMOVE THE COMPONENT
// ---------------------------
const removeComponent = (section, index) => {
  section.components.splice(index, 1);
};



// ----------------------------
// HANDLE CHANGE SECTION LAYOUT
// ----------------------------
const changeLayout = (section) => {
  section.layout_items =
    section.layout_items < 3
      ? section.layout_items + 1
      : 1
}

// ----------------------------
// HANDLE ADD SECTION POPUP
// ----------------------------
const showAddSectionPopup = ref(false)


</script>

<style lang="scss" scoped>
.project_page {
  margin-inline-start: 250px;
  padding-inline: 20px;
  .side_bar {
    padding: 20px 0;
    background: $mainColor;
    position: fixed;
    inset-inline-start: 0;
    top: 0;
    max-width: 250px;
    width: 100%;
    height: 100vh;
    z-index: 9;
    box-shadow: 0 0 10px #8483838c;
    ::-webkit-scrollbar {
      width: 2px !important;
    }
    .header_image {
      @include displayFlex();
      margin: 0 auto 20px;
      .back_btn {
        width: 40px;
        height: 40px;
        background: #fff;
        border: 1px solid #fff;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 0 8px 8px 0;
        flex-shrink: 0;
        i.pi {
          font-size: 24px;
        }
        &:hover {
          background: $mainColor;
          color: #fff;
        }
      }
      .image {
        max-width: 200px;
        padding-inline: 10px;
        + hr {
          background: #e4e4e4 !important;
        }
      }
    }

    ul.components {
      @include displayFlex($direction: column, $justify: start, $align: start);
      // margin-top: 20px;
      max-height: 90vh;
      overflow-y: scroll;
      padding-block: 20px 0px;

    }
  }

  .component_item {
    @include displayFlex($gap: 8px, $justify: start);
    padding: 20px;
    padding-inline-end: 8px;
    border: 1px solid #fff;
    width: 95%;
    color: #fff;
    margin: 0 auto;
    transition: 0.5s;
    border-radius: 4px;
    user-select: none;
    &:hover {
      background: #fff;
      color: $mainColor;
    }
    &:active {
      cursor: grabbing;
    }
    .pi:last-of-type {
      cursor: grab;
      opacity: 0.4;
      margin-inline-start: auto;
      font-size: 15px;
    }
  }


  .pages {
    @include displayFlex($justify: start, $gap: 10px);
    margin-bottom: 25px;
    .page_item {
      background: #e4e4e450;
      color: $mainColor;
      padding: 5px 10px;
      display: flex;
      align-items: center;
      gap: 15px;
      border-radius: 8px;
      transition: 0.3s;
      cursor: pointer;
      button {
        background: transparent;
        border: none;
        color: inherit;
        transform: rotate(90deg);
      }
      &:not(.active):hover {
        background: #e4e4e4;
      }
      &.active {
        background: $mainColor;
        color: #fff;
      }
      + .add_page {
        margin-inline-start: auto;
        @include circle(40px);
        border: 1px solid $mainColor;
        display: flex;
        align-items: center;
        justify-content: center;
        color: $mainColor;
        transition: 0.6s;
        i.pi {
          font-size: 15px;
          font-weight: 600;
          color: inherit;
        }
        &:hover {
          background: $mainColor;
          color: #fff;
        }
      }
    }
    + hr {
      background: #333;
      height: 3px;
    }
  }

  .project_sections {
    @include displayFlex($direction: column);
    margin-top: 20px;
    .section {
      border: 1px dashed $mainColor;
      flex-grow: 1;
      width: 100%;
      min-height: 50px;
      padding-block: 20px;
      border-radius: 4px;
      padding-inline: 20px;
      min-height: 200px;
      .section_header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-bottom: 15px;
        .section_title {
          font-size: clamp(20px, 2.5vw, 30px);
          font-weight: 500;
          padding-bottom: 8px;
        }
        .buttons {
          @include displayFlex($gap: 10px);
          button.section_control {
            min-width: 40px;
            height: 40px;
            border-radius: 4px;
            border: 1px solid $mainColor;
            font-size: 20px;
            color: $mainColor;
            padding-inline: 5px;
            &.layout_design{
              display: flex;
              align-items: center;  
              justify-content: center;
            }
            &.pi-eye{
              border-color: $dangerColor;
              color: $dangerColor;
            }
            &:hover{
              background: $mainColor;
              color: #fff;
              &.pi-eye{
                background: $dangerColor;
              }
            }
          }
        }
      }
      .content_items{
        width: 100%;
        margin-block-start: 30px;
        max-width: unset;
        .section_component{
          min-height: 66px;
          border: 1px solid #e4e4e4;
          border-radius: 8px;
          transition: 0.3s;
          display: flex;
          align-items: center;
          justify-content: center;
          color: $mainColor;
          &.drag-over {
            border: 2px dashed $mainColor;
            background: #f9f9f9;
          }
        }
      }
      &.add_section {
        cursor: pointer;
        width: 80px;
        position: fixed;
        bottom: 50px;
        right: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: unset;
        i.pi {
          font-size: 25px;
        }
        transition: 0.5s;
        &:hover {
          background: $mainColor;
          color: #fff;
        }
      }
    }
  }
}

  .drop_placeholder {
    width: 100%;
    padding: 12px;
    border: 2px dashed $mainColor;
    border-radius: 6px;
    text-align: center;
    font-size: 14px;
    opacity: 0.7;
  }
</style>
