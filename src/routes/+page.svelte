<script lang="ts">
	import { Presentation, Code, Slide, Action } from '@animotion/core'
	let code: ReturnType<typeof Code>
</script>

<Presentation>
	<Slide class="h-full place-content-center place-items-center ">
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
    monnaie(pieces,R,memo)
elif pieces[0] <= R:
    R -= pieces[0]
    memo.append(pieces[0])
    monnaie(pieces,R,memo)
print(monnaie(P,16))
			`}
			options={{ duration: 1000, stagger: 0.3, lineNumbers: true, containerStyle: false }}
		/>

		<Action do={() => code.selectLines`1`} />
		<Action do={() => code.selectLines`3-4`} />
		<Action do={() => code.selectLines`5`} />
		<Action do={() => code.selectToken`reverse`} />
		<Action do={() => code.selectLines`6-7`} />
		<Action do={() => code.selectLines`8-10`} />
		<Action do={() => code.selectLines`11-13`} />
		<Action do={() => code.selectLines`14-17`} />
		<Action do={() => code.selectLines`18`} />
		<Action do={() => code.selectLines`*`} />
		<Action do={() => code.selectLines`13,17`} />
		<Action
			do={() =>
				code.update`P = [1,3,5]
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
		/>
		<Action do={() => code.selectLines`13,17`} />
		<Action do={() => code.selectLines`*`} />
	</Slide>
	<Slide class="h-full place-content-center place-items-center">
		<p>$ python glouton.py</p>
		<p>[5, 5, 5, 1]</p>
	</Slide>
	>
	<Slide class="h-full place-content-center place-items-center">
		<p class="cursor-pointer underline decoration-5 hover:decoration-cyan-500">
			<a class="text-white no-underline" href="/animation">Voir animation</a>
		</p>
	</Slide>
</Presentation>

<style>
</style>
