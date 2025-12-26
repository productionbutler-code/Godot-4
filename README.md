# Godot-4
# gscript Character Moveent Godot 4.0

extends CharacterBody2D

@export var speed: float 120.0
@onready var sprite: AnimatedSprite2D = $AnimatedSprite2D

var facing_direction: Vector2 = Vector2.DOWN

func _physics_process(delta: float) -> void:
	var input_vector := Vector2(
		input_vector.x = Input.get_action_strength("move_r") - Input.get_action_strength("move_l")
		input_vector.y = Input.get_action_strength("move_d") - Input.get_action_strength("move_u")
	)
	#Normalize so diagonal movement
	if input_vector.length() > 0:
		input_vector = input_vector.normalized()
		facing_direction = input_vector

	velocity = input_vector * speed
	move_and_slide()

	update_animation (input_vector)

