# Introduction
This is public user documentation for V2.0 of Orbits Lua Engine. This lists everything you would need to know to start creating scripts. 
`last updated 11/14/21`

### __Menu Features__ 
Features are used to interact with the user interface, creating native-like options in the Orbit UI.
To create a new feature use `menu.add_feature(string name, string type, number parent, function)`, this returns a Feature object. The function argument is called with the feature object as an argument when the feature is pressed.

You can also add player features, these will be shown for each player in the session `menu.add_player_feature(string name, string type, number parent, function)`. Same applies for function except there is also a second argument with the target Player.

### __Feature Types__

|Type|Usage|
|-|-|
|parent|Parent feature, creates a new submenu|
|action|This is a basic feature which only has a click functionality|
|toggle|Toggle Feature|
|value_i, value_f, action_value_i, action_value_f|All of these are the same but exist for compatibility with scripts, and uses the `value` property of the Feature object|

### __Feature Object Types__
```
@ id
@ name
@ hidden
@ on
@ value
@ min
@ max
@ mod
--- Legacy Support ---
@ value_i
@ min_i
@ max_i
@ mod_i
```

### __Menu Functions__
```
Feat         add_feature(string name, string type, integer parent, function callback)
Feat         add_player_feature(string name, string type, integer parent, function callback, int playerID)
Feat         get_player_feature(int id)
bool         delete_feature(int id)
bool         delete_player_feature(int id)
string       get_version()
bool         is_trusted_mode_enabled()
void         notify(string text)
```

### __D3D Functions__
```
void         set_next_window_pos(v2 pos)
void         begin(string name, bool open, int flags)
void         end()
void         text_label(string name, string text)
void         text(string text)
bool         button(string label)
bool         selectable(string label, bool selected)
bool         slider_int(string label, int v, int min, int max)
bool         slider_float(string label, float v, float min, float max)
bool         tree_node(string label)
void         tree_pop()
void         separator()


```

### __Handlers__
```
Handler        Initialize(Feat feat, * data)
Handler        OnDxOptionsTick(Feat feat)
Handler        Tick(Feat feat, * data)
```
If you want to yield (from a script thread) you can call system.wait(i) or system.yield(i).
Script handlers are executed in a script thread, and can use game functions.
ImGui handlers are executed in the OnDxOptionsTick thread. You should only use d3d functions from these handlers.

### __Classes__

#### __Color__
|Property|Usage|Min|Max|
|-|-|-|-|
|r|Red value|0|255|
|g|Green value|0|255|
|b|Blue value|0|255|
|a|Alpha value|0|255|

#### v2 
```
@property   float       x
@property   float       y

@method v2      __add(v2|v3|float)
@method v2      __sub(v2|v3|float)
@method v2      __mul(v2|v3|float)
@method v2      __div(v2|v3|float)
@method bool    __eq(v2)
@method bool    __lt(v2)
@method bool    __le(v2)
@method string  __tostring()
@method float   magnitude(v2|nil)
```
#### v3 
```
@property   float       x
@property   float       y
@property   float       z

@constructor    v3()
@constructor    v3(float)
@constructor    v3(float, float, float)

@method v3      __add(v2|v3|float)
@method v3      __sub(v2|v3|float)
@method v3      __mul(v2|v3|float)
@method v3      __div(v2|v3|float)
@method bool    __eq(v3)
@method bool    __lt(v3)
@method bool    __le(v3)
@method string  __tostring()
@method float   magnitude(v3|nil)
@method void    transformRotToDir()
@method void    radToDeg()
@method void    degToRad()
```

### __Hook Functions__

```
hook         hook.register_script_event_hook(funtion callback)
hook         hook.register_net_event_hook(funtion callback)
bool         hook.remove_script_event_hook(int id)
bool         hook.remove_net_event_hook(int id)
```

#### __Hooks__

````
nill         script_event_hook(Player sender, int[] args, int args, int params)
nill         script_event_hook(Player sender, Player target, int eventIds)
````

___

### __RAGE__

#### __Player Functions__ 
```
Ped        get_player_ped(Player player)
Player     player_id()
void       set_player_model(Hash hash)
Group      get_player_group(Player player)
bool       is_player_female(Player player)
bool       is_player_friend(Player player)
bool       is_player_playing(Player player)
bool       is_player_free_aiming(Player player)
Entity     get_entity_player_is_aiming_at(Player player)
Vehicle    get_personal_vehicle()
void       set_player_visible_locally(Player player, bool toggle)
void       set_local_player_visible_locally(bool toggle)
void       set_player_as_modder(Player player, int flags)
string     get_player_name(Player player)
int        get_player_scid(Player player)
bool       is_player_pressing_horn(Player player)
int        get_player_ip(Player player)
bool       is_player_modder(Player player, int mask)
bool       is_player_god(Player player)
int        get_player_wanted_level(Player player)
int        player_count()
bool       is_player_in_any_vehicle(Player player)
v3         get_player_coords(Player player)
float      get_player_heading(Player player)
float      get_player_health(Player player)
float      get_player_max_health(Player player)
float      get_player_armour(Player player)
int        get_player_from_ped(Ped ped)
int        get_player_team(Player player)
Vehicle    get_player_vehicle(Player player)
bool       is_player_vehicle_god(Player player)
bool       is_player_host(Player player)
Player     get_host()
Hash       get_player_model(Player player)
bool       unset_player_as_modder(Player player, int flags)
bool       is_player_valid(Player player)
int        get_player_host_token(Player player)
void       set_player_targeting_mode(int mode)
```
#### __Ped Functions__ 
```
bool       is_ped_in_any_vehicle(Ped ped)
bool       set_group_formation(Ped group, int formation)
bool       set_ped_as_group_member(Ped ped, int groupId)
Group      get_ped_group(Ped ped)
int        get_group_size(int group)
float      get_ped_health(Ped ped)
bool       set_ped_health(Ped ped, float value)
bool       is_ped_ragdoll(Ped ped)
bool       is_ped_a_player(Ped ped)
Hash       get_current_ped_weapon(Ped ped)
bool       set_ped_into_vehicle(Ped ped, Vehicle vehicle, int seat)
int        get_ped_drawable_variation(Ped ped, int group)
int        get_ped_texture_variation(Ped ped, int group)
int        get_ped_prop_index(Ped ped, int group)
int        get_ped_prop_texture_index(Ped ped, int group)
bool       set_ped_component_variation(Ped ped, int component, int drawable, int texture, int pallette)
bool       set_ped_prop_index(Ped ped, int component, int drawable, int texture, int unk)
void       set_ped_can_switch_weapons(Ped ped, bool toggle)
bool       is_ped_shooting(Ped ped)
int        get_ped_bone_index(Ped ped, int bone)
Hash       get_ped_relationship_group_hash(Ped ped)
void       set_ped_relationship_group_hash(Ped ped, Hash hash)
Vehicle    get_vehicle_ped_is_using(Ped ped)
void       clear_all_ped_props(Ped ped)
int        clear_ped_tasks_immediately(Ped ped)
void       clear_ped_blood_damage(Ped ped)
bool       is_ped_in_vehicle(Ped ped, Vehicle vehicle)
bool       is_ped_using_any_scenario(Ped ped)
bool       set_ped_to_ragdoll(Ped ped, int time1, int time2, int type)
bool       set_ped_can_ragdoll(Ped ped, bool toggle)
bool       can_ped_ragdoll(Ped ped)
bool, v3   get_ped_last_weapon_impact(Ped ped)
bool       set_ped_combat_ability(Ped ped, BYTE ability)
float      get_ped_max_health(Entity entity)
bool       set_ped_max_health(Entity entity, float health)
bool       resurrect_ped(Ped ped)
void       set_ped_combat_movement(Ped ped, int type)
void       set_ped_combat_range(Ped ped, int type)
void       set_ped_combat_attributes(Ped ped, int attr, bool toggle)
void       set_ped_accuracy(Ped ped, int accuracy)
Ped        create_ped(int type, Hash model, v3 pos, float heading, bool isNetworked, bool unk1)
int        get_number_of_ped_drawable_variations(Ped ped, int comp)
int        get_number_of_ped_texture_variations(Ped ped, int comp, int draw)
int        get_number_of_ped_prop_drawable_variations(Ped ped, int groupId)
int        get_number_of_ped_prop_texture_variations(Ped ped, int groupId, int drawId)
void       set_ped_random_component_variation(Ped ped)
void       set_ped_default_component_variation(Ped ped)
void       set_ped_movement_clipset(Ped ped, string szClipset)
void       reset_ped_movement_clipset(Ped ped, bool unk0)
Ped        clone_ped(Ped ped)
bool       set_ped_config_flag(Ped ped, int flag, uint8_t value)
bool       set_ped_ragdoll_blocking_flags(Ped ped, int flags)
bool       reset_ped_ragdoll_blocking_flags(Ped ped, int flags)
void       set_ped_density_multiplier_this_frame(float mult)
void       set_scenario_ped_density_multiplier_this_frame(float m1, float m2)
Ped[]      get_all_peds()
Group      create_group()
void       remove_group(Group group)
void       set_ped_as_group_leader(Ped ped, Group group)
void       remove_ped_from_group(Ped ped)
bool       is_ped_group_member(Ped ped, Group group)
bool       set_group_formation_spacing(Group group, float a2, float a3, float a4)
bool       reset_group_formation_default_spacing(Group group)
void       set_ped_never_leaves_group(Ped ped, bool toggle)
bool       does_group_exist(Group group)
bool       is_ped_in_group(Ped ped)
void       set_create_random_cops(bool t)
bool       can_create_random_cops()
bool       is_ped_swimming(Ped ped)
bool       is_ped_swimming_underwater(Ped ped)
void       clear_relationship_between_groups(Hash group1, Hash group2)
void       set_relationship_between_groups(int relation, Hash group1, Hash group2)
bool       set_ped_head_blend_data(Ped ped, int shape_first, int shape_second, int shape_third, int skin_first, int skin_second, int skin_third, float mix_shape, float mix_skin, float mix_third)
float|nil  get_ped_face_feature(Ped ped, uint32_t id)
bool       set_ped_face_feature(Ped ped, uint32_t id, float val)
int|nil    get_ped_hair_color(Ped ped)
int|nil    get_ped_hair_highlight_color(Ped ped)
int|nil    get_ped_eye_color(Ped ped)
bool       set_ped_hair_colors(Ped ped, int color, int highlight)
bool       set_ped_eye_color(Ped ped, int color)
bool       set_ped_head_overlay_color(Ped ped, uint32_t overlayID, int colorType, int color, int highlight)
int|nil    get_ped_head_overlay_color_type(Ped ped, uint32_t overlayID)
int|nil    get_ped_head_overlay_color(Ped ped, uint32_t overlayID)
int|nil    get_ped_head_overlay_highlight_color(Ped ped, uint32_t overlayID)
```
#### __Entity Functions__ 
```
v3         get_entity_coords(Entity entity)
bool       set_entity_coords_no_offset(Entity entity, pos)
v3         get_entity_rotation(Entity entity)
bool       set_entity_rotation(Entity entity, v3 rot)
bool       set_entity_heading(Entity entity, float heading)
bool       set_entity_velocity(Entity entity, v3 velocity)
v3         get_entity_velocity(Entity entity)
bool       is_an_entity(Entity entity)
bool       is_entity_a_ped(Entity entity)
bool       is_entity_a_vehicle(Entity entity)
bool       is_entity_an_object(Entity entity)
bool       is_entity_dead(Entity entity)
bool       is_entity_on_fire(Entity entity)
bool       is_entity_visible(Entity entity)
bool       is_entity_attached(Entity entity)
bool       set_entity_visible(Entity entity, bool toggle)
int        get_entity_type(Entity entity)
bool       set_entity_gravity(Entity entity, bool gravity)
void       apply_force_to_entity(Ped ped, int forceType, float x, float y, float z, float rx, float ry, float rz, bool isRel, bool highForce)
Entity     get_entity_attached_to(Entity entity)
bool       detach_entity(Entity e)
Hash       get_entity_model_hash(Entity e)
float      get_entity_heading(Entity entity)
bool       attach_entity_to_entity(Entity subject, Entity target, int boneIndex, v3 offset, v3 rot, bool softPinning, bool collision, bool isPed, int vertexIndex, bool fixedRot)
void       set_entity_as_mission_entity(Entity entity, bool toggle, bool unk)
bool       set_entity_collision(Entity entity, bool toggle, bool physics, bool unk0)
bool       is_entity_in_air(Entity entity)
bool       set_entity_as_no_longer_needed(Entity entity)
bool       set_entity_no_collsion_entity(Entity entity, Entity target, bool unk)
void       freeze_entity(Entity entity, bool toggle)
bool, v3   get_entity_offset_from_coords(Entity lEntity, v3 coords)
bool, v3   get_entity_offset_from_entity(Entity lEntity, Entity lEntity2)
void       set_entity_alpha(Entity entity, int alpha, bool skin)
void       reset_entity_alpha(Entity entity)
bool       delete_entity(Entity e)
void       set_entity_god_mode(Entity entity, bool toggle)
bool       get_entity_god_mode(Entity entity)
bool       is_entity_in_water(Entity entity)
float      get_entity_speed(Entity entity)
void       set_entity_lights(Entity entity, bool toggle)
void       set_entity_max_speed(Entity entity, float speed)
float      get_entity_pitch(Entity entity)
float      get_entity_roll(Entity e)
v3         get_entity_physics_rotation(Entity e)
float      get_entity_physics_heading(Entity e)
float      get_entity_physics_pitch(Entity e)
float      get_entity_physics_roll(Entity e)
bool       does_entity_have_physics(Entity entity)
v3         get_entity_rotation_velocity(Entity entity)
float      get_entity_submerged_level(Entity entity)
int32_t    get_entity_population_type(Entity entity)
bool       is_entity_static(Entity entity)
bool       is_entity_in_zone(Entity entity, string zone)
bool       is_entity_upright(Entity entity, float angle)
bool       is_entity_upside_down(Entity entity)
bool       has_entity_been_damaged_by_any_object(Entity entity)
bool       has_entity_been_damaged_by_any_vehicle(Entity entity)
bool       has_entity_been_damaged_by_any_ped(Entity entity)
bool       has_entity_been_damaged_by_entity(Entity e1, Entity e2)
bool       does_entity_have_drawable(Entity entity)
bool       has_entity_collided_with_anything(Entity entity)
int        get_entity_bone_index_by_name(Entity entity, string name)
```
#### __Weapon Functions__ 
```
void       give_delayed_weapon_to_ped(Ped ped, Hash hash, int time, bool equipNow)
int        get_weapon_tint_count(Hash weapon)
int        get_ped_weapon_tint_index(Ped ped, Hash weapon)
void       set_ped_weapon_tint_index(Ped ped, Hash weapon, int index)
void       give_weapon_component_to_ped(Ped ped, Hash weapon, Hash component)
void       remove_all_ped_weapons(Ped ped)
void       remove_weapon_from_ped(Ped ped, Hash weapon)
bool,int   get_max_ammo(Ped ped, Hash weapon)
bool       set_ped_ammo(Ped ped, Hash weapon, int ammo)
void       remove_weapon_component_from_ped(Ped ped, Hash weapon, Hash component)
bool       has_ped_got_weapon_component(Ped ped, Hash weapon, Hash component)
Hash       get_ped_ammo_type_from_weapon(Ped ped, Hash weapon)
void       set_ped_ammo_by_type(Ped ped, Hash type, uint32_t amount)
bool       has_ped_got_weapon(Ped ped, Hash weapon)
Hash       get_all_weapon_hashes()
string     get_weapon_name(Hash weapon)
int        get_weapon_weapon_wheel_slot(Hash weapon)
Hash       get_weapon_model(Hash weapon)
Hash       get_weapon_audio_item(Hash weapon)
Hash       get_weapon_slot(Hash weapon)
int        get_weapon_ammo_type(Hash weapon)
Hash       get_weapon_weapon_group(Hash weapon)
Hash       get_weapon_weapon_type(Hash weapon)
Hash       get_weapon_pickup(Hash weapon)
```
#### __Object Functions__ 
```
Object     create_object(Hash model, v3 pos, bool networked, bool dynamic)
Object     create_world_object(Hash model, v3 pos, bool networked, bool dynamic)
Object     get_all_objects()
Pickup     get_all_pickups()
```

#### __Vehicle Functions__
```
void       set_vehicle_tire_smoke_color(Vehicle vehicle, int r, int g, int b)
Ped        get_ped_in_vehicle_seat(Vehicle vehicle, int seat)
int        get_free_seat(Vehicle vehicle)
bool       is_vehicle_full(Vehicle vehicle)
void       set_vehicle_stolen(Vehicle vehicle, bool toggle)
bool       set_vehicle_color(Vehicle v, BYTE p, BYTE s, BYTE pearl, BYTE wheel)
string     get_mod_text_label(Vehicle veh, int modType, int modValue)
string     get_mod_slot_name(Vehicle veh, int modType)
int        get_num_vehicle_mods(Vehicle veh, int modType)
bool       set_vehicle_mod(Vehicle vehicle, int modType, int modIndex, bool customTires)
int        get_vehicle_mod(Vehicle vehicle, int modType)
bool       set_vehicle_mod_kit_type(Vehicle vehicle, int type)
void       set_vehicle_extra(Vehicle veh, int extra, bool toggle)
bool       does_extra_exist(Vehicle veh, int extra)
bool       is_vehicle_extra_turned_on(Vehicle veh, int extra)
void       toggle_vehicle_mod(Vehicle veh, int mod, bool toggle)
void       set_vehicle_bulletproof_tires(Vehicle veh, bool toggle)
bool       is_vehicle_a_convertible(Vehicle veh)
bool       get_convertible_roof_state(Vehicle veh)
void       set_convertible_roof(Vehicle veh, bool toggle)
void       set_vehicle_indicator_lights(Vehicle veh, int index, bool toggle)
void       set_vehicle_brake_lights(Vehicle veh, bool toggle)
void       set_vehicle_can_be_visibly_damaged(Vehicle veh, bool toggle)
void       set_vehicle_engine_on(Vehicle veh, bool toggle, bool instant, bool noAutoTurnOn)
void       set_vehicle_fixed(Vehicle veh)
void       set_vehicle_deformation_fixed(Vehicle veh)
void       set_vehicle_undriveable(Vehicle veh, bool toggle)
bool       set_vehicle_on_ground_properly(Vehicle veh)
void       set_vehicle_forward_speed(Vehicle veh, float speed)
void       set_vehicle_number_plate_text(Vehicle veh, string text)
void       set_vehicle_door_open(Vehicle veh, int doorIndex, bool loose, bool openInstantly)
void       set_vehicle_doors_shut(Vehicle veh, bool closeInstantly)
bool       is_toggle_mod_on(Vehicle veh, int index)
void       set_vehicle_wheel_type(Vehicle veh, int type)
void       set_vehicle_number_plate_index(Vehicle veh, int index)
void       set_vehicle_tires_can_burst(Vehicle veh, bool toggle)
void       set_vehicle_tire_burst(Vehicle veh, int index, bool onRim, float unk0)
int        get_num_vehicle_mod(Vehicle veh, int modType)
bool       is_vehicle_engine_running(Vehicle veh)
void       set_vehicle_engine_health(Vehicle veh, float health)
bool       is_vehicle_damaged(Vehicle veh)
bool       is_vehicle_on_all_wheels(Vehicle veh)
Vehicle    create_vehicle(Hash model, v3 pos, float heading, bool networked, bool alwaysFalse)
bool       set_vehicle_doors_locked(Vehicle vehicle, int lockStatus)
bool       set_vehicle_neon_lights_color(Vehicle vehicle, int color)
int        get_vehicle_neon_lights_color(Vehicle vehicle)
bool       set_vehicle_neon_light_enabled(Vehicle vehicle, int index, bool toggle)
bool       is_vehicle_neon_light_enabled(Vehicle vehicle, int index, bool toggle)
void       set_vehicle_density_multipliers_this_frame(float mult)
void       set_random_vehicle_density_multiplier_this_frame(float mult)
void       set_parked_vehicle_density_multiplier_this_frame(float mult)
void       set_ambient_vehicle_range_multiplier_this_frame(float mult)
bool       is_vehicle_rocket_boost_active(Vehicle veh)
void       set_vehicle_rocket_boost_active(Vehicle veh, bool toggle)
void       set_vehicle_rocket_boost_percentage(Vehicle veh, float percentage)
void       set_vehicle_rocket_boost_refill_time(Vehicle veh, float refillTime)
void       control_landing_gear(Vehicle veh, int32_t state)
int32_t    get_landing_gear_state(Vehicle veh)
int32_t    get_vehicle_livery(Vehicle veh)
bool       set_vehicle_livery(Vehicle veh, int32_t index)
bool       is_vehicle_stopped(Vehicle veh)
int32_t    get_vehicle_number_of_passengers(Vehicle veh)
int32_t    get_vehicle_max_number_of_passengers(Vehicle veh)
int32_t    get_vehicle_model_number_of_seats(Hash modelHash)
int32_t    get_vehicle_livery_count(Vehicle veh)
int32_t    get_vehicle_roof_livery_count(Vehicle veh)
bool       is_vehicle_model(Vehicle veh, Hash model)
bool       is_vehicle_stuck_on_roof(Vehicle veh)
void       set_vehicle_doors_locked_for_player(Vehicle veh, Player player, bool toggle)
bool       get_vehicle_doors_locked_for_player(Vehicle veh, Player player)
void       set_vehicle_doors_locked_for_all_players(Vehicle veh, bool toggle)
void       set_vehicle_doors_locked_for_non_script_players(Vehicle veh, bool toggle)
void       set_vehicle_doors_locked_for_team(Vehicle veh, int32_t team, bool toggle)
void       explode_vehicle(Vehicle veh, bool isAudible, bool isInvisible)
void       set_vehicle_out_of_control(Vehicle veh, bool killDriver, bool explodeOnImpact)
void       set_vehicle_timed_explosion(Vehicle veh, Ped ped, bool toggle)
void       add_vehicle_phone_explosive_device(Vehicle veh)
bool       has_vehicle_phone_explosive_device()
void       detonate_vehicle_phone_explosive_device()
void       set_taxi_lights(Vehicle veh, bool state)
bool       is_taxi_light_on(Vehicle veh)
bool       set_vehicle_colors(Vehicle veh, int32_t primary, int32_t secondary)
bool       set_vehicle_extra_colors(Vehicle veh, int32_t pearl, int32_t wheel)
int32_t    get_vehicle_primary_color(Vehicle veh)
int32_t    get_vehicle_secondary_color(Vehicle veh)
int32_t    get_vehicle_pearlecent_color(Vehicle veh)
int32_t    get_vehicle_wheel_color(Vehicle veh)
bool       set_vehicle_fullbeam(Vehicle veh, bool toggle)
void       set_vehicle_custom_primary_colour(Vehicle veh, uint32_t color)
uint32_t   get_vehicle_custom_primary_colour(Vehicle veh)
void       clear_vehicle_custom_primary_colour(Vehicle veh)
bool       is_vehicle_primary_colour_custom(Vehicle veh)
void       set_vehicle_custom_secondary_colour(Vehicle veh, uint32_t color)
uint32_t   get_vehicle_custom_secondary_colour(Vehicle veh)
void       clear_vehicle_custom_secondary_colour(Vehicle veh)
bool       is_vehicle_secondary_colour_custom(Vehicle veh)
void       set_vehicle_custom_pearlescent_colour(Vehicle veh, uint32_t color)
uint32_t   get_vehicle_custom_pearlescent_colour(Vehicle veh)
void       set_vehicle_custom_wheel_colour(Vehicle veh, uint32_t color)
uint32_t   get_vehicle_custom_wheel_colour(Vehicle veh)
string     get_livery_name(Vehicle veh, int32_t livery)
void       set_vehicle_window_tint(Vehicle veh, int32_t t)
int32_t    get_vehicle_window_tint(Vehicle veh)
Hash       get_all_vehicle_model_hashes()
Vehicle    get_all_vehicles()
void       modify_vehicle_top_speed(Vehicle veh, float f)
void       set_vehicle_engine_torque_multiplier_this_frame(Vehicle veh, float f)
int32_t    get_vehicle_headlight_color(Vehicle v)
bool       set_vehicle_headlight_color(Vehicle v, int32_t color)
void       set_heli_blades_full_speed(Vehicle v)
void       set_heli_blades_speed(Vehicle v, float speed)
void       set_vehicle_parachute_active(Vehicle v, bool toggle)
bool       does_vehicle_have_parachute(Vehicle v)
bool       can_vehicle_parachute_be_activated(Vehicle v)
void       set_vehicle_can_be_locked_on(Vehicle veh, bool toggle, bool skipSomeCheck)
bool       set_vehicle_reduce_grip(Vehicle veh, bool t)
float      get_vehicle_estimated_max_speed(Vehicle veh)
```

#### __Streaming Functions__
```
bool       request_model(Hash hash)
bool       has_model_loaded(Hash hash)
bool       set_model_as_no_longer_needed(Hash hash)
bool       is_model_in_cdimage(Hash hash)
bool       is_model_valid(Hash hash)
bool       is_model_a_plane(Hash hash)
bool       is_model_a_vehicle(Hash hash)
bool       is_model_a_heli(Hash hash)
void       request_ipl(string szName)
void       remove_ipl(string szName)
void       request_anim_set(string szName)
bool       has_anim_set_loaded(string szName)
void       request_anim_dict(string szName)
bool       has_anim_dict_loaded(string szName)
bool       is_model_a_bike(Hash ulHash)
bool       is_model_a_car(Hash ulHash)
bool       is_model_a_bicycle(Hash ulHash)
bool       is_model_a_quad(Hash ulHash)
bool       is_model_a_boat(Hash ulHash)
bool       is_model_a_train(Hash ulHash)
bool       is_model_an_object(Hash ulHash)
bool       is_model_a_world_object(Hash ulHash)
bool       is_model_a_ped(Hash ulHash)
void       remove_anim_dict(string szName)
void       remove_anim_set(string szName)
```

#### __Gameplay Functions__
```
Hash       get_hash_key(string in)
void       display_onscreen_keyboard(string title, string default_text, int maxLength)
bool       update_onscreen_keyboard()
string     get_onscreen_keyboard_result()
bool       is_onscreen_keyboard_active()
void       set_override_weather(int weatherIndex)
void       clear_override_weather()
void       set_blackout(bool toggle)
void       set_mobile_radio(bool toggle)
int        get_game_state()
bool       is_game_state(int)
void       clear_area_of_objects(v3 coord, float radius, int flags)
void       clear_area_of_vehicles(v3 coord, float radius, bool a3, bool a4, bool a5, bool a6, bool a7)
void       clear_area_of_peds(v3 coord, float radius, bool a3)
void       clear_area_of_cops(v3 coord, float radius, bool a3)
void       set_cloud_hat_opacity(float opacity)
float      get_cloud_hat_opacity()
void       preload_cloud_hat(string szName)
void       clear_cloud_hat()
void       load_cloud_hat(string szName, float transitionTime)
void       unload_cloud_hat(string szName, float a2)
bool,float get_ground_z(v3 pos)
uint64_t   get_frame_count()
float      get_frame_time()
bool       shoot_single_bullet_between_coords(v3 start, v3 end, int32_t damage, Hash weapon, Ped owner,  bool audible, bool invisible, float speed)
```   

#### __Fire Functions__
```
bool       add_explosion(v3 pos, int type, bool isAudible, bool isInvis, float fCamShake, Ped owner)
Ped        start_entity_fire(Ped ped)
void       stop_entity_fire(Ped ped)
```

#### __Network Functions__
```
bool       network_is_host()
bool       has_control_of_entity(Entity entity)
bool       request_control_of_entity(Entity entity)
bool       is_session_started()
void       network_session_kick_player(Player player)
bool       is_friend_online(string name)
bool       is_friend_in_multiplayer(string name)
uint32_t   get_friend_scid(string name)
uint32_t   get_friend_count()
uint32_t   get_max_friends()
Hash       network_hash_from_player(Player player)
string|nil get_friend_index_name(uint32_t index)
bool       is_friend_index_online(uint32_t index)
bool       is_scid_friend(uint32_t scid)
Entity|nil get_entity_player_is_spectating(Player player)
Player|nil get_player_player_is_spectating(Player player)
bool       send_chat_message(string msg, bool teamOnly)
```
#### __Cutscene Functions__

```
void       stop_cutscene_immediately()
void       remove_cutscene()
bool       is_cutscene_active()
bool       is_cutscene_playing()
```
#### __Control Functions__
```
bool       disable_control_action(int inputGroup, int control, bool disable)
bool       is_control_just_pressed(int inputGroup, int control)
bool       is_disabled_control_just_pressed(int inputGroup, int control)
bool       is_control_pressed(int inputGroup, int control)
bool       is_disabled_control_pressed(int inputGroup, int control)
float      get_control_normal(int inputGroup, int control)
bool       set_control_normal(int inputGroup, int control, float value)
```

#### __Graphics Functions__

```
int        get_screen_height()
int        get_screen_width()
void       request_named_ptfx_asset(string asset)
bool       has_named_ptfx_asset_loaded(string asset)
void       remove_named_ptfx_asset(string name)
void       set_next_ptfx_asset(string asset)
void       set_next_ptfx_asset_by_hash(Hash hash
```
#### __Time Functions__
```
void       set_clock_time(int hour, int minute, int second)
int        get_clock_hours()
int        get_clock_minutes()
int        get_clock_seconds()
```

#### __Decorator Functions__ 
```
void       decor_register(string name, int type)
bool       decor_exists_on(Entity e, string decor)
bool       decor_remove(Entity e, string decor)
int        decor_get_int(Entity entity, string name)
bool       decor_set_int(Entity entity, string name, int value)
float      decor_get_float(Entity entity, string name)
bool       decor_set_float(Entity entity, string name, float value)
bool       decor_get_bool(Entity entity, string name)
bool       decor_set_bool(Entity entity, string name, bool value)
bool       decor_set_time(Entity entity, string name, int value)
```
#### __Interior Functions__
```
Any         get_interior_from_entity(Entity entity)
Any         get_interior_at_coords_with_type(const v3 coords, string interiorType)
void        disable_interior_prop(Any id, string prop)
void        refresh_interior(Any id)
```
#### __Water Functions__
```
float      get_waves_intensity()
void       set_waves_intensity(float intensity)
void       reset_waves_intensity()
```
#### __Stat Functions__
```
int32_t|nil stat_get_int(Hash hash, int unk0)
float|nil   stat_get_float(Hash hash, int unk0)
bool|nil    stat_get_bool(Hash hash, int unk0)
bool        stat_set_int(Hash hash, int32_t value, bool save)
bool        stat_set_float(Hash hash, float value, bool save)
bool        stat_set_bool(Hash hash, bool value, bool save)
```

#### __Cam Functions__
```
v3          get_gameplay_cam_rot()
v3          get_gameplay_cam_pos()
float       get_gameplay_cam_relative_pitch()
float       get_gameplay_cam_relative_yaw()
```

#### __UI Functions__
```
 Entity             get_entity_from_blip(Blip blip)
 Blip               get_blip_from_entity(Entity entity)
 Blip               add_blip_for_entity(Entity entity)
 bool               set_blip_sprite(Blip blip, int spriteId)
 bool               set_blip_colour(Blip blip, int colour)
 void               hide_hud_component_this_frame(int componentId)
 void               hide_hud_and_radar_this_frame()
 string             get_label_text(string label)
 void               draw_rect(float x, float y, float width, float height, int r, int g, int b, int a)
 void               draw_line(v3 pos1, v3 pos2, int r, int g, int b, int a)
 void               draw_text(string pszText, v2 pos)
 void               set_text_scale(float scale)
 void               set_text_color(int r, int g, int b, int a)
 void               set_text_font(int font)
 void               set_text_wrap(float start, float end)
 void               set_text_outline(bool b)
 void               set_text_centre(bool b)
 void               set_text_right_justify(bool b)
 void               set_text_justification(int j)
 void               set_new_waypoint(v2 coord)
 v2                 get_waypoint_coord()
 bool               is_hud_component_active(int32_t componentId)
 void               show_hud_component_this_frame(int32_t componentId)
 void               set_waypoint_off()
 bool               set_blip_as_mission_creator_blip(Blip blip, bool toggle)
 bool               is_mission_creator_blip(Blip blip)
 Blip               add_blip_for_radius(v3 pos, float radius)
 Blip               add_blip_for_pickup(Pickup pickup)
 Blip               add_blip_for_coord(v3 pos)
 void               set_blip_coord(Blip blip, v3 coord)
 v3                 get_blip_coord(Blip blip)
 bool               remove_blip(Blip blip)
 void               set_blip_route(Blip blip, bool toggle)
 void               set_blip_route_color(Blip blip, int32_t color)
```

#### __Sound Functions__
```
void       play_sound(int soundId, string audioName, string audioRef, bool p4, Any p5, bool p6)
void       play_sound_frontend(int soundId, string audioName, string audioRef, bool p4)
void       play_sound_from_entity(int soundId, string audioName, Entity entity, string audioRef)
void       play_sound_from_coord(int soundId, string audioName, v3 pos, string audioRef, bool a5, int range, bool a7)
void       stop_sound(int soundId)
```
#### __Ai Fuctions__ 
```
void      task_goto_entity(Entity e, Entity target, int duration, float distance, float speed)
bool      task_combat_ped(Ped ped, Ped target, int a3, int a4)
Any       task_go_to_coord_by_any_means(Ped ped, v3 coords, float speed, Any p4, bool p5, int walkStyle, float a7)
bool      task_wander_standard(Ped ped, float unk0, bool unk1)
void      task_vehicle_drive_wander(Ped ped, Vehicle vehicle, float speed, int driveStyle)
void      task_start_scenario_in_place(Ped ped, string name, int unkDelay, bool playEnterAnim)
void      task_start_scenario_at_position(Ped ped, string name, v3 coord, float heading, int duration, bool sittingScenario, bool teleport)
void      task_stand_guard(Ped ped, v3 coord, float heading, string name)
void      play_anim_on_running_scenario(Ped ped, string dict, string name)
bool      does_scenario_group_exist(string name)
bool      is_scenario_group_enabled(string name)
bool      set_scenario_group_enabled(string name, bool b)
void      reset_scenario_groups_enabled()
bool      set_exclusive_scenario_group(string name)
bool      reset_exclusive_scenario_group()
bool      is_scenario_type_enabled(string name)
bool      set_scenario_type_enabled(string name, bool b)
void      reset_scenario_types_enabled()
bool      is_ped_active_in_scenario(Ped ped)
void      task_follow_to_offset_of_entity(Ped ped, Entity entity, v3 offset, float speed, int timeout, float stopRange, bool persistFollowing)
void      task_vehicle_drive_to_coord_longrange(Ped ped, Vehicle vehicle, v3 pos, float speed, int mode, float stopRange)
void      task_shoot_at_entity(Entity entity, Entity target, int duration, Hash firingPattern)
void      task_vehicle_escort(Ped ped, Vehicle vehicle, Vehicle targetVehicle, int mode, float speed, int drivingStyle, float minDistance, int a8, float noRoadsDistance)
void      task_vehicle_follow(Ped driver, Vehicle vehicle, Entity targetEntity, float speed, int drivingStyle, int minDistance)
void      task_vehicle_drive_to_coord(Ped ped, Vehicle vehicle, v3 coord, float speed, int a5, Hash vehicleModel, int driveMode, float stopRange, float a9)
void      task_vehicle_shoot_at_coord(Ped ped, v3 coord, float a3)
void      task_vehicle_shoot_at_ped(Ped ped, Ped target, float a3)
void      task_vehicle_aim_at_coord(Ped ped, v3 coord)
void      task_vehicle_aim_at_ped(Ped ped, Ped target)
void      task_stay_in_cover(Ped ped)
void      task_go_to_coord_while_aiming_at_coord(Ped ped, v3 gotoCoord, v3 aimCoord, float moveSpeed, bool a5, float a6, float a7, bool a8, Any flags, bool a10, Hash firingPattern)
void      task_go_to_coord_while_aiming_at_entity(Ped ped, v3 gotoCoord, Entity target, float moveSpeed, bool a5, float a6, float a7, bool a8, Any flags, bool a10, Hash firingPattern)
void      task_go_to_entity_while_aming_at_coord(Ped ped, Entity gotoEntity, v3 aimCoord, float a4, bool shoot, float a6, float a7, bool a8, bool a9, Hash firingPattern)
void      task_go_to_entity_while_aiming_at_entity(Ped ped, Entity gotoEntity, Entity target, float a4, bool shoot, float a6, float a7, bool a8, bool a9, Hash firingPattern)
void      task_open_vehicle_door(Ped ped, Vehicle vehicle, int timeOut, int doorIndex, float speed)
void      task_enter_vehicle(Ped ped, Vehicle vehicle, int timeout, int seat, float speed, uint32_t flag, Any p6)
void      task_leave_vehicle(Ped ped, Vehicle vehicle, uint32_t flag)
void      task_sky_dive(Ped ped, bool a2)
void      task_parachute(Ped ped, bool a2, bool a3)
void      task_parachute_to_target(Ped ped, v3 coord)
void      set_parachute_task_target(Ped ped, v3 coord)
void      set_parachute_task_thrust(Ped ped, float thrust)
void      task_rappel_from_heli(Ped ped, float a2)
void      task_vehicle_chase(Ped driver, Entity target)
void      set_task_vehicle_chase_behaviour_flag(Ped ped, int flag, bool set)
void      set_task_vehicle_chase_ideal_persuit_distance(Ped ped, float dist)
void      task_shoot_gun_at_coord(Ped ped, v3 coord, int duration, Hash firingPattern)
void      task_aim_gun_at_coord(Ped ped, v3 coord, int time, bool a4, bool a5)
void      task_turn_ped_to_face_entity(Ped ped, Entity entity, int duration)
void      task_aim_gun_at_entity(Ped ped, Entity entity, int duration, bool a4)
bool      is_task_active(Ped ped, Any taskId)
bool      task_play_anim(Ped ped, string dict, string anim, float speed, float speedMult, int duration, int flag, float playbackRate, bool lockX, bool lockY, bool lockZ)
void      stop_anim_task(Ped ped, const char* dict, const char* anim, float a4)
```

#### __Script Functions__
```
void      trigger_script_event(int eventId, Player player, int[] params)
```

#### __System Functions__
```
void      yield(int ms)
void      wait(int ms)
```