<script lang="ts">
    import {
        ListBox,
        ListBoxItem,
        Table,
        tableMapperValues,
    } from "@skeletonlabs/skeleton";
    import type {
        PaginationSettings,
        TableSource,
    } from "@skeletonlabs/skeleton";
    import { Avatar } from "@skeletonlabs/skeleton";
    import { TabGroup, Tab, TabAnchor } from "@skeletonlabs/skeleton";
    import { Autocomplete } from "@skeletonlabs/skeleton";
    import type { AutocompleteOption } from "@skeletonlabs/skeleton";
    import { Paginator } from "@skeletonlabs/skeleton";
    import { popup } from "@skeletonlabs/skeleton";
    import type { PopupSettings } from "@skeletonlabs/skeleton";

    const sourceData = [
        { position: 1, name: "Mã cuộc gọi", description: "81aa42-12f6" },
        { position: 2, name: "Điện thoại viên", description: "admin@t4vn" },
        { position: 3, name: "Thời gian ", description: "11/09/2024 03:27:00" },
        { position: 4, name: "Thời lượng", description: "5 phút 20 giây" },
    ];

    const sourceResult = [
        { position: 1, name: "Cảm xúc chung cuộc", status: "Good" },
        { position: 2, name: "Cảm xúc khách hàng", status: "Good" },
        { position: 3, name: "Cảm xúc điện thoại viên", status: "Normal" },
        { position: 4, name: "Trạng thái kết thúc", status: "Good" },
    ];

    const sourceHistory = [
        {
            position: 1,
            stt: "1",
            script: "abc",
            time: "12/9/2024 08:55:01",
            person: "Tự động",
            maxPoint: "100",
            point: "75",
            ratePoint: "75%",
            rating: "Đạt",
        },
        {
            position: 2,
            stt: "2",
            script: "1234",
            time: "12/9/2024 09:05:59",
            person: "Tự động",
            maxPoint: "100",
            point: "30",
            ratePoint: "30%",
            rating: "Trượt",
        },
    ];

    const tableSimple: TableSource = {
        head: ["Thông tin cuộc gọi"],
        body: tableMapperValues(sourceData, ["name", "description"]),
        meta: tableMapperValues(sourceData, [
            "position",
            "name",
            "description",
        ]),
    };

    const tableEmotion: TableSource = {
        head: [],
        body: tableMapperValues(sourceResult, ["name", "status"]),
        meta: tableMapperValues(sourceResult, ["position", "name", "status"]),
    };

    const tableHistory: TableSource = {
        head: [
            "Stt",
            "Kịch bản",
            "Thời gian xử lý",
            "Người chấm",
            "Điểm tối đa",
            "Điểm",
            "Tỉ lệ điểm",
            "Đánh giá",
        ],
        body: tableMapperValues(sourceHistory, [
            "stt",
            "script",
            "time",
            "person",
            "maxPoint",
            "point",
            "ratePoint",
            "rating",
        ]),
        meta: tableMapperValues(sourceHistory, [
            "position",
            "stt",
            "script",
            "time",
            "person",
            "maxPoint",
            "point",
            "ratePoint",
            "rating",
        ]),
    };

    let tabSet: number = 0;

    let paginationSettings = {
        page: 0,
        limit: 5,
        size: sourceHistory.length,
        amounts: [1, 2, 5, 10],
    } satisfies PaginationSettings;

    let comboboxValue: string;

    const popupCombobox: PopupSettings = {
        event: "click",
        target: "popupCombobox",
        placement: "top",
        closeQuery: ".listbox-item",
    };
</script>

<ol class="breadcrumb">
    <li class="crumb">
        <a class="anchor" href="#">Request List</a>
    </li>
    <li class="crumb-separator" aria-hidden="true">&rsaquo;</li>
    <li>Details</li>
</ol>

<div class="home flex justify-between">
    <div class="left-side w-1/3">
        <Table
            source={tableSimple}
            class="custom-table card p-4 shadow-md rounded-xl"
        />

        <div class="card p-4 shadow-md mt-4 rounded-xl">
            <span class="font-bold text-lg">Transcript</span>
            <audio controls class="w-full">
                <source src="" type="audio/mpeg" />
                Your browser does not support the audio element.
            </audio>
            <div class="grid grid-rows-[1fr_auto] gap-1">
                <div class="bg-surface-500/30 p-4 overflow-y-auto">
                    <div class="grid grid-cols-[1fr_auto] gap-2">
                        <div
                            class="card p-4 rounded-tr-none space-y-2 white bg-blue-400 rounded-l-xl rounded-br-xl"
                        >
                            <header
                                class="flex justify-between items-center text-white"
                            >
                                <p class="font-bold">Điện thoại viên</p>
                                <small class="opacity-80">16:18</small>
                            </header>
                            <p class="text-white">
                                Hello, how can i help you ??
                            </p>
                        </div>
                        <Avatar
                            src="https://moc247.com/wp-content/uploads/2023/12/loa-mat-voi-101-hinh-anh-avatar-meo-cute-dang-yeu-dep-mat_2.jpg"
                            width="w-12"
                        />
                    </div>
                </div>
                <div class="bg-surface-500/30 p-4 overflow-y-auto">
                    <div class="grid grid-cols-[auto_1fr] gap-2">
                        <Avatar
                            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTqZVmnksw_4Y_u8fE30KMN3FcFdHVcPdsfEPpiZl4sb9oqP39xsvNy1TX2nFi_WMMMA-U&usqp=CAU"
                            width="w-12"
                        />
                        <div
                            class="card p-4 variant-soft rounded-tl-none space-y-2 black bg-gray-200 rounded-e-xl rounded-bl-xl"
                        >
                            <header class="flex justify-between items-center">
                                <p class="font-bold">Khách hàng</p>
                                <small class="opacity-80">16:20</small>
                            </header>
                            <p>
                                Yeah i need to find something, can you help me
                                ??
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="right-side w-3/5">
        <div class="card p-4 shadow-md rounded-xl">
            <h2 class="font-bold text-lg border-b border-zinc-400">
                Kết quả quality control
            </h2>
            <TabGroup>
                <Tab bind:group={tabSet} name="tab1" value={0}>Cảm xúc</Tab>
                <Tab bind:group={tabSet} name="tab2" value={1}>Từ khóa</Tab>
                <!-- Tab Panels --->
                <svelte:fragment slot="panel">
                    {#if tabSet === 0}
                        <Table
                            source={tableEmotion}
                            class="w-1/2 custom-table table-emotion"
                        />
                    {:else if tabSet === 1}
                        (tab panel 2 contents)
                    {/if}
                </svelte:fragment>
            </TabGroup>
        </div>
        <div class="card p-4 shadow-md mt-4 rounded-xl">
            <h2 class="font-bold text-lg">Lịch sử chấm điểm</h2>

            <div class="flex justify-between">
                <div>
                    <input
                        class="input w-1/3 h-full border-zinc-400"
                        type="search"
                        name="demo"
                        placeholder="Search..."
                    />

                    <button
                        class="btn variant-filled justify-between border-2 border-zinc-400"
                        use:popup={popupCombobox}
                    >
                        <span class="capitalize"
                            >{comboboxValue ?? "Trigger"}</span
                        >
                        <span>↓</span>
                    </button>
                    <div
                        class="card w-48 shadow-xl py-2 bg-white"
                        data-popup="popupCombobox"
                    >
                        <ListBox rounded="rounded-none">
                            <ListBoxItem
                                bind:group={comboboxValue}
                                name="medium"
                                value="books">Books</ListBoxItem
                            >
                            <ListBoxItem
                                bind:group={comboboxValue}
                                name="medium"
                                value="movies">Movies</ListBoxItem
                            >
                            <ListBoxItem
                                bind:group={comboboxValue}
                                name="medium"
                                value="television">TV</ListBoxItem
                            >
                        </ListBox>
                        <div class="arrow bg-surface-100-800-token" />
                    </div>

                    <button
                        type="button"
                        class="btn variant-filled border-2 border-zinc-400"
                    >
                        <span>(icon)</span>
                        <span>Run</span>
                    </button>
                    <button
                        type="button"
                        class="btn variant-filled border-2 border-zinc-400"
                    >
                        <span>(icon)</span>
                        <span>Reset</span>
                    </button>
                </div>
                <button
                    type="button"
                    class="btn variant-filled bg-orange-600 text-white"
                >
                    Chấm thủ công
                </button>
            </div>
            <Table source={tableHistory} class="custom-table" />

            <Paginator
                class="mt-3"
                bind:settings={paginationSettings}
                showFirstLastButtons={false}
                showPreviousNextButtons={true}
            />
        </div>
    </div>
</div>
