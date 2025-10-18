<script lang="ts">
	import * as Sidebar from '$lib/components/ui/sidebar/index.js';
	import DashboardIcon from '@tabler/icons-svelte/icons/dashboard';
	import DeviceDesktopIcon from '@tabler/icons-svelte/icons/device-desktop';
	import DeviceGamepad2Icon from '@tabler/icons-svelte/icons/device-gamepad-2';
	import ShieldCheckIcon from '@tabler/icons-svelte/icons/shield-check';
	import AlertTriangleIcon from '@tabler/icons-svelte/icons/alert-triangle';
	import BookIcon from '@tabler/icons-svelte/icons/book';
	import BrandDiscordIcon from '@tabler/icons-svelte/icons/brand-discord';
	import TicketIcon from '@tabler/icons-svelte/icons/ticket';
	import NavUser from '@/components/sidebar/nav-user.svelte';
	import NavHeader from '@/components/sidebar/nav-header.svelte';
	import LogoHorizontal from '@/assets/images/logo-horizontal.png';

	const data = {
		user: {
			name: 'User',
			email: 'user@example.com',
			avatar: '/avatars/shadcn.jpg'
		}
	};
</script>

<Sidebar.Provider
	style="--sidebar-width: calc(var(--spacing) * 72); --header-height: calc(var(--spacing) * 12);"
>
	<Sidebar.Root collapsible="offcanvas" variant="inset">
		<Sidebar.Header>
			<Sidebar.Menu>
				<Sidebar.MenuItem>
					<Sidebar.MenuButton class="data-[slot=sidebar-menu-button]:!p-1.5">
						<img src={LogoHorizontal} alt="Logo" class="m-0.5 h-8 w-auto" />
					</Sidebar.MenuButton>
				</Sidebar.MenuItem>
			</Sidebar.Menu>
		</Sidebar.Header>
		<Sidebar.Content>
			<!-- Dashboard -->
			<Sidebar.Group>
				<Sidebar.GroupContent>
					<Sidebar.Menu>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Dashboard">
								{#snippet child({ props })}
									<a {...props} href="/panel">
										<DashboardIcon />
										<span>Dashboard</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
					</Sidebar.Menu>
				</Sidebar.GroupContent>
			</Sidebar.Group>

			<!-- Servers Section -->
			<Sidebar.Group>
				<Sidebar.GroupLabel>Servers</Sidebar.GroupLabel>
				<Sidebar.GroupContent>
					<Sidebar.Menu>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="VPS Servers">
								{#snippet child({ props })}
									<a {...props} href="/panel/vps-servers">
										<DeviceDesktopIcon />
										<span>VPS Servers</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Game Servers">
								{#snippet child({ props })}
									<a {...props} href="/panel/game-servers">
										<DeviceGamepad2Icon />
										<span>Game Servers</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
					</Sidebar.Menu>
				</Sidebar.GroupContent>
			</Sidebar.Group>

			<!-- Protection Section -->
			<Sidebar.Group>
				<Sidebar.GroupLabel>Protection</Sidebar.GroupLabel>
				<Sidebar.GroupContent>
					<Sidebar.Menu>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Remote Protection">
								{#snippet child({ props })}
									<a {...props} href="/panel/remote-protection">
										<ShieldCheckIcon />
										<span>Remote Protection</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Alerts">
								{#snippet child({ props })}
									<a {...props} href="/panel/alerts">
										<AlertTriangleIcon />
										<span>Alerts</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
					</Sidebar.Menu>
				</Sidebar.GroupContent>
			</Sidebar.Group>

			<!-- Help Section -->
			<Sidebar.Group>
				<Sidebar.GroupLabel>Help</Sidebar.GroupLabel>
				<Sidebar.GroupContent>
					<Sidebar.Menu>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Tickets">
								{#snippet child({ props })}
									<a {...props} href="/panel/tickets">
										<TicketIcon />
										<span>Tickets</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Docs">
								{#snippet child({ props })}
									<a {...props} href="/panel/docs">
										<BookIcon />
										<span>Docs</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
						<Sidebar.MenuItem>
							<Sidebar.MenuButton tooltipContent="Discord">
								{#snippet child({ props })}
									<a {...props} href="/panel/discord">
										<BrandDiscordIcon />
										<span>Discord</span>
									</a>
								{/snippet}
							</Sidebar.MenuButton>
						</Sidebar.MenuItem>
					</Sidebar.Menu>
				</Sidebar.GroupContent>
			</Sidebar.Group>
		</Sidebar.Content>
		<Sidebar.Footer>
			<NavUser user={data.user} />
		</Sidebar.Footer>
	</Sidebar.Root>

	<Sidebar.Inset>
		<NavHeader />
		<div class="flex flex-1 flex-col">
			<div class="@container/main flex flex-1 flex-col gap-2">
				<div class="flex flex-col gap-4 py-4 md:gap-6 md:py-6">
					<slot />
				</div>
			</div>
		</div>
	</Sidebar.Inset>
</Sidebar.Provider>
