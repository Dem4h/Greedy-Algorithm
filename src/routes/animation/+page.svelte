<script lang="ts">
	import { Presentation, Code, Slide, Action } from '@animotion/core'
	import { tween } from '@animotion/motion'

	const coins = $state([
		{ tween: tween({ x: 0, fill: '#ffd700', scale: 1 }), val: 1, viewBox: '-150 -50 300 300' },
		{ tween: tween({ x: 0, fill: '#ffd700', scale: 1 }), val: 2, viewBox: '-150 -50 300 300' },
		{ tween: tween({ x: 0, fill: '#ffd700', scale: 1 }), val: 5, viewBox: '-150 -50 300 300' }
	])
	let text = tween({ scale: 1, val: 16 })
	async function animation0() {
		await coins[0].tween.to({ x: 400 })
		coins[0].val = 5
		await coins[2].tween.to({ x: -400 })
		coins[2].val = 1
		coins[0].tween.to({ x: 0 })
		coins[2].tween.to({ x: 0 })
	}

	async function animation1() {
		await text.to({ scale: 3 })
		await text.to({ scale: 1 })
	}

	async function animation2() {
		await coins[0].tween.to({ fill: 'red', scale: 3 })
		await coins[0].tween.to({ fill: '#ffd700', scale: 1 }, { delay: 600 })
	}

	async function animation3() {
		await coins[0].tween.to({ fill: 'green', scale: 3 })
		await coins[0].tween.to({ fill: '#ffd700', scale: 1 }, { delay: 600 })
	}
	async function animation4() {
		await text.to({ scale: 2 })
		await text.to({ val: 11 })
		await text.to({ scale: 1 })
	}
	async function animation5() {
		await text.to({ scale: 2 })
		await text.to({ val: 6 })

		await text.to({ scale: 1 })
	}
	async function animation6() {
		await text.to({ scale: 2 })
		await text.to({ val: 1 })
		await text.to({ scale: 1 })
	}
	async function animation7() {
		await coins[1].tween.to({ fill: 'green', scale: 3 })
		await coins[1].tween.to({ fill: '#ffd700', scale: 1 }, { delay: 600 })
	}
	async function animation8() {
		await coins[2].tween.to({ fill: 'green', scale: 3 })
		await coins[2].tween.to({ fill: '#ffd700', scale: 1 }, { delay: 600 })
	}
	async function animation9() {
		await text.to({ scale: 2 })
		await text.to({ val: 0 })
		await text.to({ scale: 1 })
	}
	let code: ReturnType<typeof Code> = $state()
</script>

<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<Presentation class="h-full w-full">
	<Slide class="absolute h-full w-full place-content-center text-3xl ">
		<div class="grid h-full w-full grid-cols-3 grid-rows-1">
			<div class=" flex">
				{#each coins as coin}
					<svg style="scale: {coin.tween.scale};" class="relative" viewBox={coin.viewBox}>
						<circle cx={coin.tween.x} cy={100} r={50} fill={coin.tween.fill} />
						<text
							x={coin.tween.x}
							y={100}
							class="h-fit w-fit"
							font-family="Monaspace Neon"
							font-size="48px"
							text-anchor="middle"
							dominant-baseline="middle"
						>
							{coin.val}
						</text>
					</svg>
				{/each}
			</div>
			<div class="flex">
				<Code
					bind:this={code}
					lang="python"
					theme="poimandres"
					code={`P = [1,3,5]
def monnaie(pieces,R,memo=None):
    if memo is None:
memo = []
pieces.sort(reverse=True)
if len(pieces) == 0:
    return "impossible"
elif R == 0:
    return memo
    pieces = []
elif pieces[0] > R:
    del pieces[0]
    return monnaie(pieces,R,memo)
elif pieces[0] <= R:
    R -= pieces[0]
    memo.append(pieces[0])
    return monnaie(pieces,R,memo)
print(monnaie(P,16))
					`}
					options={{ duration: 1000, stagger: 0.3, lineNumbers: true, containerStyle: false }}
				/>
			</div>
			<div
				style="scale: {text.scale}"
				class="flex flex-col justify-center text-xl lg:text-3xl xl:text-7xl 2xl:text-9xl"
			>
				{text.val.toFixed(0)}
			</div>
		</div>
		<Action do={() => code.selectLines`1`} />

		<Action do={() => code.selectLines`3-4`} />
		<Action do={() => code.selectLines`5`} />
		<Action do={() => code.selectToken`reverse`} />
		<Action do={animation0} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`8-10`} />
		<Action do={animation1} />
		<Action do={() => code.selectLines`11-13`} />
		<Action do={animation2} />
		<Action do={() => code.selectLines`14-17`} />
		<Action do={animation3} />
		<Action do={animation4} />
		<!-- 2nd execution-->
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`5`} />
		<Action do={() => code.selectToken`reverse`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`8-10`} />
		<Action do={animation1} />
		<Action do={() => code.selectLines`11-13`} />
		<Action do={animation2} />
		<Action do={() => code.selectLines`14-17`} />
		<Action do={animation3} />
		<Action do={animation5} />
		<!-- 3rd-->
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`14-17`} />
		<Action do={animation3} />
		<Action do={animation6} />
		<!-- 4th-->
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`11-13`} />
		<Action do={animation3} />
		<!-- 5th-->
		<Action do={() => coins[0].tween.to({ x: -1000 })} />
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`11-13`} />
		<Action do={animation7} />
		<Action do={() => coins[1].tween.to({ x: -1000 })} />

		<!-- 6th -->
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`14-17`} />
		<Action do={animation8} />
		<Action do={animation9} />
		<!-- 7th-->
		<Action do={() => code.selectLines`2`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`8-10`} />
	</Slide>
</Presentation>

<style>
</style>
