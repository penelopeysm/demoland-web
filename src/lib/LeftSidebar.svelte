<script lang="ts">
    import Sidebar from "src/lib/Sidebar.svelte";
    import Tooltip from "src/lib/reusable/Tooltip.svelte";
    import showWelcomeIcon from "src/assets/show-welcome.svg";
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    import Choose from "src/lib/leftSidebar/Choose.svelte";
    import Create from "src/lib/leftSidebar/Create.svelte";
    import Import from "src/lib/leftSidebar/Import.svelte";
    import Welcome from "src/lib/leftSidebar/Welcome.svelte";
    import Tabs from "src/lib/leftSidebar/Tabs.svelte";
    import { config } from "src/config";

    import { scenarioName, compareScenarioName } from "src/stores";
    let welcomeVisible: boolean = !(
        localStorage.getItem("doNotShowWelcome") === "true"
    );

    let selectedTab: "choose" | "create" | "import" = "choose";

    // This function fires when a new scenario is successfully added, either
    // via Create (custom scenarios) or Import (file upload).
    function handleImportEvent(event: CustomEvent) {
        selectedTab = "choose";
        $scenarioName = event.detail.name;
        $compareScenarioName = null;
        dispatch("changeScenario");
    }
</script>

<Welcome bind:welcomeVisible />
<Sidebar>
    <div class="sidebar-contents">
        <h1 class="yuuuuuuge">A</h1>
    </div>
</Sidebar>

<style>
    div.sidebar-contents {
        /* This controls the total width of the left sidebar. */
    }

    h1.yuuuuuuge {
        font-size: 4000%;
        font-weight: 700;
        margin: 40px 80px;
        text-align: center;
        font-family: "Dancing Script", cursive;
    }

    h1.title {
        margin-top: 0px !important;
    }

    button#show-welcome {
        background-color: transparent;
        border: none;
        cursor: pointer;
        padding: 0;
        height: 15px;
        width: 15px;
        transform: translateY(2px);
    }
    button#show-welcome:hover {
        background-color: #dddddd;
    }
    button#show-welcome > img {
        height: 100%;
        width: 100%;
    }

    div#tabs-and-content {
        margin-top: 20px;
    }
    div.tab-content {
        padding: 10px 10px 12px 10px;
        border: 1px solid #e6e6e6;
        border-radius: 0px 0px 6px 6px;
        background-color: #ffffff;
    }
</style>
