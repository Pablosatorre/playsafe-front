<script lang="ts">
	import LogoHorizontal from '$lib/assets/images/logo-horizontal.png';
	import BackgroundImage from '$lib/assets/images/PLAYSAFE-07.jpg';
	import {
		FieldGroup,
		Field,
		FieldLabel,
		FieldDescription,
		FieldSeparator
	} from '$lib/components/ui/field/index.js';
	import { Input } from '$lib/components/ui/input/index.js';
	import { Button } from '$lib/components/ui/button/index.js';
	import { Card, CardContent, CardHeader } from '$lib/components/ui/card/index.js';

	let email = '';
	let password = '';
</script>

<svelte:head>
	<title>Sign In - PlaySafe</title>
</svelte:head>

<div class="grid h-svh lg:grid-cols-2 overflow-hidden">
	<div class="flex flex-col gap-4 p-6 md:p-8">
		<div class="flex justify-center gap-2 md:justify-start">
			<a href="/" class="flex items-center gap-2 font-medium transition-opacity hover:opacity-80">
				<img src={LogoHorizontal} alt="Logo" class="h-8 w-auto" />
			</a>
		</div>
		<div class="flex flex-1 items-center justify-center">
			<Card class="w-full max-w-md border-border/50 shadow-2xl backdrop-blur">
				<CardHeader class="space-y-2 pb-3 pt-5">
					<div class="flex flex-col items-center gap-2 text-center">
						<div
							class="rounded-2xl bg-gradient-to-br from-primary/20 to-primary/5 p-2.5 mb-1 ring-1 ring-primary/10"
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="w-7 h-7 text-primary"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z"
								/>
							</svg>
						</div>
						<div class="space-y-1">
							<h1
								class="text-2xl font-bold tracking-tight bg-gradient-to-r from-foreground to-foreground/70 bg-clip-text"
							>
								Welcome back
							</h1>
							<p class="text-muted-foreground text-balance text-sm">
								Choose your preferred sign in method
							</p>
						</div>
					</div>
				</CardHeader>
				<CardContent class="pb-5">
					<form class="space-y-3.5">
						<FieldGroup>
							<!-- Social Login Buttons -->
							<div class="grid grid-cols-2 gap-3">
								<Button
									variant="outline"
									type="button"
									class="w-full h-10 hover:bg-accent hover:border-primary/30 transition-all"
								>
									<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-4 h-4 mr-2">
										<path
											fill="currentColor"
											d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"
										/>
										<path
											fill="currentColor"
											d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"
										/>
										<path
											fill="currentColor"
											d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"
										/>
										<path
											fill="currentColor"
											d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"
										/>
									</svg>
									Google
								</Button>
								<Button
									variant="outline"
									type="button"
									class="w-full h-10 hover:bg-accent hover:border-primary/30 transition-all"
								>
									<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-4 h-4 mr-2">
										<path
											fill="currentColor"
											d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515a.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0a12.64 12.64 0 0 0-.617-1.25a.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057a19.9 19.9 0 0 0 5.993 3.03a.078.078 0 0 0 .084-.028a14.09 14.09 0 0 0 1.226-1.994a.076.076 0 0 0-.041-.106a13.107 13.107 0 0 1-1.872-.892a.077.077 0 0 1-.008-.128a10.2 10.2 0 0 0 .372-.292a.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127a12.299 12.299 0 0 1-1.873.892a.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028a19.839 19.839 0 0 0 6.002-3.03a.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.956-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.955-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.946 2.418-2.157 2.418z"
										/>
									</svg>
									Discord
								</Button>
							</div>

							<FieldSeparator class="my-3.5">Or continue with email</FieldSeparator>

							<!-- Email and Password Fields -->
							<div class="space-y-2.5">
								<Field>
									<FieldLabel for="email" class="text-sm font-medium">Email address</FieldLabel>
									<Input
										id="email"
										type="email"
										placeholder="you@example.com"
										bind:value={email}
										required
										class="h-10"
									/>
								</Field>
								<Field>
									<div class="flex items-center justify-between mb-1.5">
										<FieldLabel for="password" class="text-sm font-medium">Password</FieldLabel>
										<a
											href="/auth/forgot-password"
											class="text-xs text-primary font-medium hover:underline underline-offset-4 transition-colors"
										>
											Forgot password?
										</a>
									</div>
									<Input
										id="password"
										type="password"
										bind:value={password}
										required
										class="h-10"
									/>
								</Field>
							</div>

							<!-- Login Button -->
							<Button
								type="submit"
								class="w-full h-10 text-sm font-medium shadow-lg shadow-primary/25 hover:shadow-xl hover:shadow-primary/30 transition-all mt-1.5"
							>
								<svg
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewBox="0 0 24 24"
									stroke-width="1.5"
									stroke="currentColor"
									class="w-4 h-4 mr-2 flex-shrink-0"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										d="M15.75 9V5.25A2.25 2.25 0 0013.5 3h-6a2.25 2.25 0 00-2.25 2.25v13.5A2.25 2.25 0 007.5 21h6a2.25 2.25 0 002.25-2.25V15m3 0l3-3m0 0l-3-3m3 3H9"
									/>
								</svg>
								<span>Sign in</span>
							</Button>

							<!-- Sign Up Link -->
							<div class="relative mt-3.5">
								<div class="absolute inset-0 flex items-center">
									<div class="w-full border-t border-border/40"></div>
								</div>
								<div class="relative flex justify-center text-xs">
									<span class="bg-background px-3 text-muted-foreground"> New to PlaySafe? </span>
								</div>
							</div>

							<a
								href="/register"
								class="inline-flex items-center justify-center w-full h-10 px-4 rounded-md border border-dashed border-input bg-background text-sm font-medium hover:bg-accent hover:text-accent-foreground hover:border-solid transition-all"
							>
								<svg
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewBox="0 0 24 24"
									stroke-width="1.5"
									stroke="currentColor"
									class="w-4 h-4 mr-2 flex-shrink-0"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										d="M19 7.5v3m0 0v3m0-3h3m-3 0h-3m-2.25-4.125a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zM4 19.235v-.11a6.375 6.375 0 0112.75 0v.109A12.318 12.318 0 0110.374 21c-2.331 0-4.512-.645-6.374-1.766z"
									/>
								</svg>
								<span>Create new account</span>
							</a>
						</FieldGroup>
					</form>
				</CardContent>
			</Card>
		</div>
	</div>
	<div class="bg-muted relative hidden lg:block overflow-hidden">
		<div
			class="absolute inset-0 bg-gradient-to-br from-primary/20 via-background/10 to-primary/10 z-10"
		></div>
		<img
			src={BackgroundImage}
			alt="Background"
			class="absolute inset-0 h-full w-full object-cover"
		/>
		<div class="absolute inset-0 flex items-center justify-center z-20 p-12">
			<div class="max-w-lg text-center space-y-6">
				<div
					class="inline-flex items-center justify-center p-4 rounded-full bg-primary/10 backdrop-blur-xl border border-primary/20 mb-4"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="w-12 h-12 text-primary"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"
						/>
					</svg>
				</div>
				<div
					class="space-y-4 backdrop-blur-sm bg-background/30 p-8 rounded-2xl border border-primary/20"
				>
					<h2 class="text-4xl font-bold text-foreground leading-tight">
						Your Shield Against<br />DDoS Attacks
					</h2>
					<p class="text-lg text-foreground/80">
						Enterprise-grade protection that keeps your servers safe and your players connected,
						24/7.
					</p>
					<div class="flex items-center justify-center gap-8 pt-4">
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">99.9%</div>
							<div class="text-sm text-muted-foreground">Uptime</div>
						</div>
						<div class="h-12 w-px bg-border"></div>
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">24/7</div>
							<div class="text-sm text-muted-foreground">Protection</div>
						</div>
						<div class="h-12 w-px bg-border"></div>
						<div class="text-center">
							<div class="text-3xl font-bold text-primary">500+</div>
							<div class="text-sm text-muted-foreground">Servers</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
